## Migrating Matlab code to Python

> This is part 3 of my guide on transitioning from Matlab to Python. Read [part 1: a curriculum to learn Python](https://xcorr.net/2020/02/21/transitioning-away-from-matlab/) and [part 2: choosing environments, IDEs and packages](https://xcorr.net/2020/02/29/orienting-yourself-through-python/).

So you're beginning to use Python daily. Great! You might still have a critical set of Matlab scripts from back in the day that doesn't have a neat equivalent in Python. How do you rewrite this code in Python without introducing many headaches? I've had to do this a handful of times and have developed a method based on test-driven development that avoids the biggest issues in code translation::

1. Define what we want to translate
2. Create a test plan based on existing code
3. Write tests in Python
4. Write the code in Python
5. Iterate until tests pass

To test the method, I've migrated a script that I found in [Susillo and Abbott (2009)](https://www.ncbi.nlm.nih.gov/pubmed/19709635). It simulates a chaotic neural network and trains it with recursive least-squares. I wanted to make sure I would run into issues (gotchas!) when I translated the code to exercise the method - and I did!

### Pick your battles

Algorithmic code that does matrix manipulation is typically a good candidate for translation into Python. Importantly, the code you will translate needs to currently run in Matlab, since we're going to have to run the code and capture its current behaviour.

Try to avoid direct translation of code with dependencies on Simulink, GUIDE, or esoteric toolboxes. For GUIDE in particular, I've found that the limitations of GUIDE enforce a certain style of coding - lots of globals and convoluted logic. You're probably better off rewriting the GUI code from scratch than attempting direct translation. 

Not every piece of Matlab code needs to be translated to Python. If your goal is to archive an existing pipeline so it continues to run despite deprecation, [containerizing Matlab with Docker](https://github.com/mathworks-ref-arch/matlab-dockerfile) is a good route. You can also call legacy Matlab code from Python directly using the official Matlab engine for Python from Mathworks or using shell calls. However, some situations will *require* translating Matlab code, for instance if you want to run your code in the cloud. 

Finally, consider doing the process for a smaller project first. It's not that easy! You will learn a lot from doing this once on a smaller scale. I recommend that you [create a git repo for your project and commit regularly](https://swcarpentry.github.io/git-novice/), because you might be doing a lot of iterations to get everything to run correctly.

### Creating a test-based strategy for rewriting the code

We've identified a good script or function to rewrite. Should we start writing Python? No! It is very easy to rewrite code in another language that *seems* to work, but has subtle bugs. You can spend days or weeks chasing down these bugs, and it will drive you crazy! For this reason, we will use a test-based strategy:

1. Capture what the behaviour of the code is *right now* for a variety of inputs.
2. Rewrite the code in Python and make sure it does exactly the thing that we want it to do. That is, for the same inputs, it gives us the same outputs.

[We will create unit tests to verify the behaviour of our code is correct](https://en.wikipedia.org/wiki/Unit_testing), meaning that is matches the old code exactly. At this point you may say - *hold on, I don't just want to transfer the code over, I want to improve it*! Our goal is to capture the logic part of the code - the number-crunching. This does not stop us from improving the reference code in a number of ways, including:

* Making constants changeable
* Making the code more modular
* Using Pythonic data structures, for example using `pandas` to store time series.

In any case, we have to build on a solid foundation - a reference. Once we replicate the original behaviour and commit it to a repo, we can improve it later in a new commit.

### Identify inputs and outputs

We need to identify the inputs and outputs of the script or function we want to rewrite. One very nice thing about Matlab is that functions tend to be stateless and do not modify their arguments (unless an input is a reference object type, which is pretty rare). Thus, we can reason pretty easily about the inputs and the outputs to a function: 

* The inputs are the arguments.
* The outputs are the return variables.

Functions may have side-effects, such as creating a plot or saving a file. A side-effect to a function is [an observable effect besides returning a value (the main effect) to the invoker of the operation](https://en.wikipedia.org/wiki/Side_effect_(computer_science)). If the code you're translating has side-effects, you should aim to remove them. 

For example, consider a function takes in data and returns nothing, saving the results to disk, like so:

```matlab
function []=mycomplexop(outfile)
    data = zeros(100, 100);
    % Complex things happen in the middle...
    save(outfile, 'data')
end
```

You can transform this into a side-effect-free function by returning the results instead of saving them:

```matlab
function [data]=mycomplexop()
    data = zeros(100, 100);
    % Complex things happen in the middle...
    return;
end
```

I prefer to comment out plotting code rather than trying to replicate it exactly. Again, we want to focus on the number crunching.

### Identify test cases

Many Matlab scripts are written in a style where the inputs to a function are set up, a function or set of functions are called, and then the output is plotted. We need to capture the inputs to this set of functions as well as the inputs. An easy way to do this is using `save`:

```matlab
% Set up the inputs.
t = 0:1000
dt = .1
g = 10

save inputs.mat -hdf5

% Call the function
complexoutput = mycomplexfun(t, dt, g);

save outputs.mat -hdf5

% Plotting the
plot(t, complexoutput)
```

I used Octave here - but you can use `-v7.3` rather than `-hdfd5` to save if you're using Matlab. `mat` files saved in these formats are actually hdf5 files that Python can read.

Pay special attention to randomization. It will be hard to replicate Matlab's random number generation exactly in Python. Ideally, functions should be independent of randomizations, because functions with random outputs are very hard to test for correctness. If a function requires random variables to implement an algorithm, we can circumvent this issue by giving the function the random data it needs. For example, let's say we have a function that computes the distribution of the range of a random normal variable:

```matlab
function [dist] = rangedist()
    A = randn(100, 1000);
    dist = max(A, 1) - min(A, 1);
end
```

We can rewrite this function so that its source of randomness comes from outside the function:

```matlab
function [dist] = rangedist(A)
    dist = max(A, 1) - min(A, 1);
end
```

Then we can generate the `A` variable in a script, and save that particular random draw. 

Make sure to pick test cases that won't take more than a few seconds to run. You will be running your tests many times, and these seconds will add up! Toy data is fine. It's also good practice to test our code on simple inputs where the correct output is clear, for example, all zeros, all ones, etc. Save as many input-output pairs as is necessary to capture the range of behaviours of functions you want to capture.

In addition to testing our script end-to-end, we may choose to test intermediate computations involved in the script. Testing more fine-grained computations will help you debug your code. If your function is already written as a function, it may call private functions - which can make things a bit tricky. You may need to refactor a bit of the Matlab code to make private functions public, so that you can capture both their inputs and outputs. 

### Writing a test scaffold

Unit testing checks whether the results of a function are as expected given a set of inputs. Testing in Python can range from using simple inline `assert` statements to sophisticated automated solutions that check that tests pass every time you push code into your repo. In our case, we will use a lightweight manual testing method: hiding test cases behind `__name__ == '__main__'`. 

We will create a python module that is meant to be imported, for example, via `import mymodule`. When we run the file on the command line, however, via `python module.py`, the code hidden behind this `if` statement will be run:

```python
import numpy as np

def my_complex_fun(A):
    # Complicated things occur.
    return A * 2

def _run_tests():
    # Load inputs.
    with h5py.File('inputs.mat', 'r') as f:
        A = np.array(f['A/value'])

    with h5py.File('outputs.mat', 'r') as f:
        B_ref = np.array(f['B/value'])

    # Call the function.
    B = my_complex_fun(A)

    # Check shapes are good.
    assert A.shape == B.shape

    # Check values are similar.
    np.testing.assert_all_close(B, B_ref)

if __name__ == '__main__':
    # Run the tests.
    _run_tests()
```

The tests are inside the `_run_tests()` function. This way, the module namespace will not be polluted with variables that could have the same name as other variables inside of function.

When the code is run, the tests should raise errors if the output is not as expected, which will stop execution. You will see a big old error on the command line, and then you know that you must correct the code. You can raise an error by:

* Using the `assert` statement. It raises an error whenever the statement is False. 
* Using the methods in [`np.testing`](https://docs.scipy.org/doc/numpy/reference/routines.testing.html). These methods can check whether, for example, a numpy array's elements are all close to a reference (within numeric error).
* Using the `raise` statement to manually raise an error.

That's really all you need to test code. [Numerous unit-testing libraries in Python exist](https://realpython.com/python-testing/), but at their core is the same idea: create code that raises an error when the output not what is expected. 

### Picking organization

Main effects are much easier to test than side effects in the unit-testing framework. You'll often find yourself writing side-effect-free, modular and functional code for this reason. That's great! You'll tend to create smaller functions so that you can test each individual component. Your code will be easier to reason about. 

The Python code you write may be objected-oriented. Although Matlab now has excellent support for classes, much Matlab code, especially older code, eschews the use of classes. If you don't feel comfortable writing object-oriented code, don't sweat it - Python code doesn't have to use classes to be Pythonic. Classes make sense when something needs to remember and manage its own state. [Here's a tutorial on Python classes if it's something that intrigues you](https://realpython.com/python3-object-oriented-programming/).

### Writing the code - common gotchas

Now that we've picked our tests, and picked how we'll organize our code, we can start coding. Matlab's matrix operations naturally translate to Numpy. Be careful with these common gotchas:

* Reshape operations will cause you headaches. Matlab uses Fortran order, Python uses C by default. This means in Matlab:

```matlab
A = [1, 2, 3; 4, 5, 6]
A(:)

ans = 
    [1, 4, 2, 5, 3, 6]
```

Whereas in Python:

```python
>>> A = np.array([[1, 2, 3], [4, 5, 6]])
>>> print(A.ravel())
[1, 2, 3, 4, 5, 6]
```

* Saving to hdf5 in Matlab and loading in Python will invert axes because of the distinction between C and Fortran order. You will have to swap axes front to back, for example. For example, if you save a three-dimensional tensor in Matlab `A` and then load it back in Python via hdf5, you will need to call `A.swapaxes((2, 1, 0))` to get back the original tensor.
* Be careful with dimension-one vectors! If you have a one-dimension vector `a` of shape `(N, )`, then `a.dot(a.T)` gives you a vector of the shape `(N, )`. It will not be a scalar, nor a matrix. If you wanted to computed the outer product of `a` with itself, use `a.reshape((-1, 1)).dot(a.reshape((1, -1)))` or better yet `np.outer(a, a)`.
* Hidden dot products can cause problems! The `*` operator applies to scalars and to vectors in Matlab, and the semantics are different depending on the dimension of the operands. `A.dot(B)` replace Matlab's `A * B`. [You may also see `A @ B` being used but it's still rather esoteric](https://www.python.org/dev/peps/pep-0465/). * Objects in Python have pass-by-reference semantics. Several methods in numpy modify data in place. Be careful! Sometimes, you will explictly need to `copy()` your data.
* Python uses 0-based indices and Matlab 1-based indices. Watch out!
* Look at your data! Don't fly blind!

If you write a piece of code that you suspect may cause a bug, you can use inline `assert` statements to make sure it works. I like to use this to check the dimensions of intermediate arrays, for example. 

Some of the problems of direct index manipulation can go away by using `pandas` dataframes where appropriate. [`xarray`](http://xarray.pydata.org/en/stable/) uses named dimensions for tensors, which can help avoid many mistakes caused by the need of swapping axes and reshaping. [`np.einsum`](https://docs.scipy.org/doc/numpy/reference/generated/numpy.einsum.html) can express complicated sums and products of tensors in an easy-to-read, less error-prone manner.

You might want to consider translating parts of your numerics to [PyTorch](https://pytorch.org/) or [Tensorflow](https://www.tensorflow.org/) directly, especially if you want to take advantage of automatic differentiation. Performance-sensitive code can be JIT'ed using [jax](https://github.com/google/jax) or [numba](https://numba.pydata.org/), or rewritten in [Cython](https://cython.org/). Start small and optimize as necessary.

### Using the method on a real script

[The example script I rewrote is about 165 lines of code](https://github.com/patrickmineault/test-driven-migration/original_force_external_feedback_loop.m). It's written in a pedagogic style and intersperses explanations, logic and plotting. In that sense, it's similar to a jupyter notebook. I focused on  transferring the logic of the main loop, which does a forward simulation of the network and trains it with the FORCE algorithm. 

I had to change a handful of things related to plotting to get it to run in Octave, but I was able to get it to run within about 10 minutes. Not bad for 10-year code! The code is organized in this way:

* sets up variables.
* runs the body of the computation (a big for loop). This body has side effects (plotting).
* finishes in an end state that contain the results of the computation.

Although the code is not set up as a function, it was fairly easy to isolate the inputs are - they're what the `for` loop needs to get started:

* `x0`, `z0`, `wf`, `dt`, `M`, `N`, `ft`

And the outputs are the variables computed in the main for loop, namely:

* `zt` and `w0_len`

I captured these inputs and outputs as a test case for my script. I commented out the forward simulation of the trained network that comes after the main for loop, since it's another logically separate component of the code that I could attack later. 

In addition to the end-to-end result of the script, I captured the result of the first iteration of forwarding the network state, to create a more granular test. I also checked array dimensions.

I decided to write the code as a class, with methods `train` and `simulate`. [The resulting code doesn't look like Matlab code](https://github.com/patrickmineault/test-driven-migration/blob/master/chaotic_rnn.py). Yet, because I'd set up a test scaffold, I could be assured that it works the same as the old Matlab code. 

Translation was hard! I ran into multiple very subtle issues translating the rather short code I was working (maybe 20 lines of real logic). The issues were subtle - incorrect manipulation of dimension-1 vectors, off by 1 errors in  loops. Having reference code and functional tests allowed me to isolate these issues, fix them, and replicate the original functionality exactly. It took about 3 hours, which is a lot! I was very careful to set up a well-defined goalpost when I translated the code, so I knew when I would be done, which kept me going.

[The translated code is available here](https://github.com/patrickmineault/test-driven-migration/blob/master/chaotic_rnn.py). [I imported the code into a notebook and generated some figures from it](https://github.com/patrickmineault/test-driven-migration/blob/master/Use%20chaotic%20RNN.ipynb) - it runs! 

### Conclusion

Using test-driven development, it's possible to systematically, incrementally transfer legacy Matlab code to the Python environment. You can be assured that the code will *work* in the end, because you will have defined what working means. You will have created a test suite for your code with good coverage for your new Python code. You might even have spottle subtle bugs in the original Matlab code along the way! These are all noble goals in their own way.


