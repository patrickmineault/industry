### Migrating Matlab code to Python

So you're beginning to use Python in your day to day. Great! You might still have a critical set of scripts from back in the day that doesn't have a neat equivalent in Python. How do you rewrite this code in Python without introducing many headaches?

I've had to do this a handful of times and have developed a framework to avoid the biggest issues in code translation. Throughout this article I will show how to migrate a script that I found in Susillo and Abbott (2009) that looks at how to train chaotic neural networks with recursive least-squares. 

It's a really great paper, and I highly recommend you have a look. The example code is in Matlab, and what it does is set up a chaotic RNN, trains it to generate a specific input with the FORCE algorithm, and then plots it. A copy of the original script is here.

#### Pick your battles

The script I will transfer is about 170 lines of code. It's written in a pedagogic style and intersperses explanations, logic and plotting. In that sense it's similar to a jupyter notebook. The thing I really want to focus on is transferring over the logic of the main loop, which does a forward simulation of the network and trains it with the FORCE algorithm. The plotting and explanations aren't as tricky. The logic part is a reasonable target to try to migrate to Python:

* it's relatively circumscribed. The whole script is 170 lines, but the meat of the `for`, which does the tricky (and interesting) numerics is only about 20 lines. 
* it doesn't have any dependencies on Simulink, GUIDE or an esoteric Matlab toolbox
* it runs - I had to change a handful of things related to plotting to get it to run in Octave, but I was able to get it to run within about 10 minutes. Not bad for 10-year code! We're going to need to run the code with different inputs in order to rewrite it in another language.

I've commented out the forward simulation of the trained network that comes after the main for loop, since it's another logically separate component of the code I can attack later.

The strategy I am advocating can work for larger codebases - larger codebases can be split out into manageable subpieces that can be dealt with separately.

#### Creating a test-based strategy for rewriting the code

We've identified a good script or function to rewrite. Should we start writing Python? No! It is very easy to rewrite code in another language that *seems* like it works but has subtle bugs. You can spend days or weeks chasing down these bugs, and it will drive you crazy! For this reason, we will use a test-based strategy:

* We will capture what the behaviour of the code is right now for a variety of inputs.
* We will rewrite the code in Python and make sure it does exactly the thing that we want it to do. That is, for the same inputs it gives us the same outputs.

[We will create unit tests to verify the behaviour of our code is correct](https://en.wikipedia.org/wiki/Unit_testing), meaning that is matches the old code exactly. At this point you may say - hold on, I don't just want to transfer the code over, I want to improve it! Our goal is to capture the logic part of the code - the number crunching. This does not stop us from improving the old code in a number of ways, including:

* Making the organization better
* Making constants changeable
* Using more appropriate data structures

In any case, we have to build on a solid foundation - a reference. Once you replicate the original behaviour and commit it to a repo, we can improve it later in a new commit.

#### Identify inputs and outputs

We need to identify the inputs and outputs of the script or function we want to rewrite. One very nice thing about Matlab is that functions tend to be stateless and do not modify their arguments (unless an input is a reference object type, which is pretty rare). Thus, we can reason pretty easily about the inputs to the function and the outputs: 

* The inputs are the arguments.
* The outputs are the return variables.

Functions may have side-effects, such as creating a plot or saving a file. A side-effect to a function is [an observable effect besides returning a value (the main effect) to the invoker of the operation](https://en.wikipedia.org/wiki/Side_effect_(computer_science)). If the code is not side-effect free, you should aim to remove them. 

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

* sets up variables
* runs the body of the computation (a big for loop). This body has many side effects (plotting)
* finishes in an end state

Although the code is not set up as a function, it's fairly easy to find out what the inputs are - they're what the `for` loop needs to get started:

TODO: change these

* `x0` and `z0`

And the outputs are the variables computed in the main for loop, namely:

* `zt` and `w0_len`

#### Identify test cases

The next step is to identify the test cases we want to focus on. In the chaotic RNN case, there's already a test case in the test script. The script generates its inputs and then shows us the output. A simple way capture what the function receives as inputs and returns as outputs is to call to `save` before and after the the main loop:

```matlab
save inputs.mat -hdf5
for t = simtime
    % Many lines of code here...
end
save outputs.mat -hdf5
```

I am using Octave here - but you can use `-v7.3` instead if you're using Matlab. mat files saved in these formats are actually hdf5 files that Python can read.

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

Then we can generate the `A` variable inside of a script, and save that particular random draw. 

Make sure to pick test cases that won't take more than a few seconds to run. I've decided to remove to decrease `N` from 1000 to 200 for this purpose in the chaotic RNN script for this purpose. You will be running your tests many times, and these seconds will add up! Toy data is fine.

#### Writing a test scaffold

* Testing can range from very simple (assert) to using PyUnit to using Jenkins.
* We'll pick something simple - writing the test case behind `__name__ == '__main__'`. 
* We write our test first
* We write our code to satisfy the test

#### Picking organization

* We could write the code as a function, a class or whatever else we feel like
* When we do test-driven development, we often need to write functions and classes that are easy to test
* Sometimes this will mean, for example, putting the body of a for loop inside of its own function, so we can test one iteration.
* In my case, I've decided to write the code as a class that initializes parameters by itself. I can then run it for an arbitrary number of iterations by calling simulate(). The code doesn't look like Matlab code - it's quite Pythonic - yet because we've set up a test scaffold we can be assured that it works the same as the old Matlab code.

#### Writing the code

* Could use numpy or another framework, like PyTorch, Tensorflow, or jax. It's up to us.
* This part is the easiest - with a good scaffold, if you rewrite the code and it produces the right outputs, you can have peace of mind that it actually works.

#### Gotchas

* Saving to hdf5 will invert the axes -> you will have to swap axes front to back to get the original matrix
* Be careful with dimension one vectors! 
* Hidden dot products can cause headaches! Sometimes * means multiply, other times it means dot product. Check the dimensions of the intermediate products and sprinkle liberally with asserts.
* a.dot(a.T) gives you a vector of the shape a, not a scalar (if a was a row vector) or a matrix (if a was a column vector). Check your dimensions.
* Look at your data! Don't fly blind!
* Split the computations into elementary functions. Then test these functions rather the whole function, end-to-end.

#### Conclusion

Here's the final code. It real pretty!


