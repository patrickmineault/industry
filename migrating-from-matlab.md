## Migrating Matlab code to Python

> This is part 3 of my guide on transitioning from Matlab to Python. Read [parts 1](https://xcorr.net/2020/02/21/transitioning-away-from-matlab/) and [2](https://xcorr.net/2020/02/29/orienting-yourself-through-python/).

So you're beginning to use Python daily. Great! You might still have a critical set of scripts from back in the day that doesn't have a neat equivalent in Python. How do you rewrite this code in Python without introducing many headaches? I've had to do this a handful of times and have developed a method based on test-driven development that avoids the biggest issues in code translation. The basic idea is to:

1. Define what we want to translate
2. Create a test plan based on the existing code
3. Write tests in Python
4. Write the code in Python and iterate until tests pass

Throughout this article I will illustrate these concepts by migrating a particular script that I found in [Susillo and Abbott (2009)](https://www.ncbi.nlm.nih.gov/pubmed/19709635). It simulates a chaotic neural network and trains it with recursive least-squares. It's a really great paper, and I highly recommend you have a look. [A copy of the original script is here](https://github.com/patrickmineault/test-driven-migration/original_force_external_feedback_loop.m).

### Pick your battles

The example script I will transfer is about 165 lines of code. It's written in a pedagogic style and intersperses explanations, logic and plotting. In that sense, it's similar to a jupyter notebook. I really want to focus on is transferring over the logic of the main loop, which does a forward simulation of the network and trains it with the FORCE algorithm. The plotting and explanations aren't as tricky. The logic part is a reasonable target to try to migrate to Python:

* it's relatively circumscribed. The whole script is 165 lines, but the core of the `for` loop, which does the tricky  numerics, is only about 20 lines. 
* it doesn't have any dependencies on Simulink, GUIDE or an esoteric Matlab toolbox
* it runs - I had to change a handful of things related to plotting to get it to run in Octave, but I was able to get it to run within about 10 minutes. Not bad for 10-year code! We're going to need to run the code with different inputs in order to rewrite it in another language.

I've commented out the forward simulation of the trained network that comes after the main for loop, since it's another logically separate component of the code that I could choose to attack later. The strategy I am advocating can work for larger codebases. These larger codebases can be split out into manageable subpieces that can be dealt with separately.

### Creating a test-based strategy for rewriting the code

We've identified a good script or function to rewrite. Should we start writing Python? No! It is very easy to rewrite code in another language that *seems* like it works but has subtle bugs. You can spend days or weeks chasing down these bugs, and it will drive you crazy! For this reason, we will use a test-based strategy:

* We will capture what the behaviour of the code is *right now* for a variety of inputs.
* We will rewrite the code in Python and make sure it does exactly the thing that we want it to do. That is, for the same inputs, it gives us the same outputs.

[We will create unit tests to verify the behaviour of our code is correct](https://en.wikipedia.org/wiki/Unit_testing), meaning that is matches the old code exactly. At this point you may say - hold on, I don't just want to transfer the code over, I want to improve it! Our goal is to capture the logic part of the code - the number crunching. This does not stop us from improving the reference code in a number of ways, including:

* Making constants changeable
* Making the code more modular
* Using Pythonic data structures, for example using `pandas` to store time series.

In any case, we have to build on a solid foundation - a reference. Once we replicate the original behaviour and commit it to a repo, we can improve it later in a new commit.

### Identify inputs and outputs

We need to identify the inputs and outputs of the script or function we want to rewrite. One very nice thing about Matlab is that functions tend to be stateless and do not modify their arguments (unless an input is a reference object type, which is pretty rare). Thus, we can reason pretty easily about the inputs to the function and the outputs: 

* The inputs are the arguments.
* The outputs are the return variables.

Functions may have side-effects, such as creating a plot or saving a file. A side-effect to a function is [an observable effect besides returning a value (the main effect) to the invoker of the operation](https://en.wikipedia.org/wiki/Side_effect_(computer_science)). If the code has side-effects, you should aim to remove them. 

For example, consider a function takes in data and returns nothing, saving the results to disk, like so:

```matlab
function []=mycomplexop(outfile)
    data = zeros(100, 100);
    % Complex things happen in the middle...
    save(outfile, 'data')
end
```

You can transform this into a side-effect free function by returning the results instead of saving them:

```matlab
function [data]=mycomplexop()
    data = zeros(100, 100);
    % Complex things happen in the middle...
    return;
end
```

In our case, the example code we have isn't wrapped in a function. Instead, it is a script that:

* sets up variables.
* runs the body of the computation (a big for loop). This body has side effects (plotting).
* finishes in an end state that contain the results of the computation.

Although the code is not set up as a function, it's fairly easy to find out what the inputs are - they're what the `for` loop needs to get started:

* `x0`, `z0`, `wf`, `dt`, `M`, `N`, `ft`

And the outputs are the variables computed in the main for loop, namely:

* `zt` and `w0_len`

### Identify test cases

The next step is to identify the test cases we want to focus on. In the chaotic RNN case, there's already a test case in the test script. The script generates its inputs and then shows us the output. A simple way to capture what the function receives as inputs and returns as outputs is to call to `save` before and after the the main loop:

```matlab
save inputs.mat -hdf5
for t = simtime
    % Many lines of code here...
end
save outputs.mat -hdf5
```

I used Octave here - but you can use `-v7.3` instead if you're using Matlab. mat files saved in these formats are actually hdf5 files that Python can read.

We have to pay special attention to randomization. It will be hard to replicate Matlab's random number generation exactly in Python. We should thus strive to make our functions independent of randomization. If a function requires random variables to implement an algorithm, we can circumvent this issue by giving the function the random data it needs. For example, let's say we have a function that computes the distribution of the range of a random normal variable:

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

Then we can generate the `A` variable in of a script, and save that particular random draw. 

Make sure to pick test cases that won't take more than a few seconds to run. I've decided to decrease `N` from 1000 to 200 for this purpose in the chaotic RNN script for this purpose. You will be running your tests many times, and these seconds will add up! Toy data is fine.

In addition to testing our script end-to-end, we may choose to test intermediate computations involved in the script. Testing more fine-grained computations will help you debug your code. If your function is already written as a function, it may call private functions - which can make things a bit tricky. You may need to refactor a bit of the Matlab code to make private functions public, so that you can capture both their inputs and outputs. In our running example, I captured the result of the first iteration of forwarding the network state.

### Writing a test scaffold

Unit testing checks whether the results of a function are as expected given a set of inputs. Testing in Python can range from using simple inline `assert` statements to sophisticated automated solutions that check that tests pass every time you push code into your repo. In our case, we will use a lightweight manual testing method: hiding test cases behind `__name__ == '__main__'`. We will create a python module that is meant to be imported, for example, via `import chaotic_rnn`. When we run the file on the command line, however, via `python chaotic_rnn.py`, the code hidden behind this `if` statement will be run:

```python
import numpy as np

class ChaoticRnn:
    def __init__(self):
        self.t = 0
        pass

    # Many more lines of code here.

if __name__ == '__main__':
    # Run the tests.
    instance = ChaoticRnn()
    assert instance.t == 0

    # ...more test here...
```

When our code is incorrect, the tests should raise errors, which will stop execution. You will see a big old error on the command line, and then you know that you must correct the code. You can raise an error by:

* Using the `assert` statement. It raises an error whenever the statement is False. 
* Using the methods in [`np.testing`](https://docs.scipy.org/doc/numpy/reference/routines.testing.html). These methods can check whether, for example, a numpy array's elements are all close to a reference (within numeric error).
* Using the `raise` statement to manually raise an error.

That's really all you need to test code. [Numerous unit-testing libraries in Python exist](https://realpython.com/python-testing/), but at their core is the same idea: create code that raises an error when the output not what is expected.

### Picking organization

Main effects are much easier to test than side effects in the unit-testing framework. You'll often find yourself writing side-effect-free, modular and functional code for this reason. That's great! Your code will tend to be easier to reason about. You'll also tend to create smaller functions so that you can test each individual component. 

Your Python code you write may be objected-oriented; although Matlab now has excellent support for classes, much Matlab code, especially older code, eschews the use of classes. In my case, I've decided to write the code as a class that initializes parameters by itself. I can then run it for an arbitrary number of iterations by calling simulate(). The code doesn't look like Matlab code - it's quite Pythonic - yet because we've set up a test scaffold we can be assured that it works the same as the old Matlab code.

### Writing the code

Now that we've picked our tests, and picked how we'll organize our code, we can start coding. Matlab's matrix operations naturally translate to Numpy. Be careful with these common gotchas:

* Saving to hdf5 in Matlab and loading in Python will invert axes because of the distinction between C and Fortran order. This will cause you endless headaches. You will have to swap axes front to back, for example. For example, if you save a three-dimensional tensor in Matlab `A` and then load it back in Python via hdf5, you will need to call `A.swapaxes((2, 1, 0))` to get back the original tensor.
* Be careful with dimension-one vectors! If you have a one-dimension vector `a` of shape `(N, )`, then a.dot(a.T) gives you a vector of the shape `(N, )`. It will not be a scalar nor a matrix. If you wanted to computer the outer product of `a` with itself, use `a.reshape((-1, 1)).dot(a.reshape((1, -1)))`.
* Hidden dot products can cause problems! The `*` operator applies to scalars and to vectors in Matlab, and the semantics are different depending on the dimension of the operands. Check the dimensions of the intermediate products with `assert` statements.
* Objects in Python have pass-by-reference semantics. Several methods in numpy modify data in place. Be careful! Sometimes, you will explictly need to `copy()` your data.
* Look at your data! Don't fly blind!

You might want to consider translating parts of your numerics to [PyTorch](https://pytorch.org/) or [Tensorflow](https://www.tensorflow.org/) directly, especially if you want to take advantage of automatic differentiation. Performance-sensitive code can be JIT'ed using [jax](https://github.com/google/jax) or [numba](https://numba.pydata.org/), or rewritten in [Cython](https://cython.org/). Start small and optimize as necessary.

#### Conclusion

I ran into multiple issues translating the rather short code I was working. The issues were subtle - incorrect manipulation of dimension-1 vectors, off by 1 errors. Having reference code and functional tests allowed me to isolate these issues, fix them, and replicate the original functionality exactly. 

[The translated code is available here](https://github.com/patrickmineault/test-driven-migration/blob/master/chaotic_rnn.py). I imported the code into a notebook and ran on some example here. 

Is your codebase is too big to translate to Python? Perhaps you would prefer to take a snapshot of your current pipeline and call it inside of a virtual environment. Running Matlab in Docker is tricky but it could keep your legacy pipelines running for the next decade. Curious? Write a comment below - if there is enough interest I will write a new article about it.


