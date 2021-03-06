## Transitioning away from Matlab

[In my last article](https://xcorr.net/2020/02/18/how-i-got-a-job-in-industry/), I talked about how I got a job in industry. I had been programming Python on and off for 10 years when I got my first non-academic job. Having proficiency in a language that people use outside of academia will improve your chances of getting a job in industry. Learning a new language will also grow your abilities as a programmer and will unlock new projects and analyses you might have otherwise been afraid to tackle. 

What if you're in a lab that's been using Matlab for years and you haven't had a chance to learn Python? Here's my guide to transition off of Matlab to Python. There are a few specific links to neuroscience at the end of the article, but it should be useful to anybody approaching Python from a Matlab background.

### Learn Python the hard way

Python is one of the most popular languages out there - [more popular than Matlab by a factor of at least 10](http://pypl.github.io/PYPL.html) - and it's the language the vast majority people transitioning from Matlab will choose. There's two basic strategies you can apply here:

* Transfer learning (aka the easy way). You have things in Matlab you use every day - array operations, plotting, signal processing, etc. You learn to do the same thing in Python, [perhaps with the aid of a cheatsheet](https://cheatsheets.quantecon.org/). A lot of the Python data science API (numpy, scipy and matplotlib in particular) are very  similar to Matlab. They were originally built to replicate functionality in Matlab. With this route you'll get moderately productive very fast. 
* Starting from scratch (aka the hard way). Learn the syntax, then do something you couldn't do in Matlab, for example:
  * Learn algorithms and data structures
  * Make a GUI application (e.g. in PyQT)
  * Make a game
  * Make a dynamic website

My *slightly* controversial opinion is you're better off starting from scratch. If you use the transfer learning method you will be less productive than you currently are for a long time. You will feel annoyed at your own incompetence (*"why am I doing this to myself? I could do the same thing twice as fast!"*). Furthermore, you will have a tendency of doing things *the Matlab way* (using matrices for everything, index chaining, avoiding for loops) that are error-prone and you shouldn't be doing in a general purpose programming language. 

By starting from scratch you will learn new things you couldn't do before at all - you will feel like you have new powers. You can write a GUI! You can make dynamic visualizations! You can make games! You can do deep learning! Your day-to-day productivity won't suffer because you'll be learning *new* skills instead of relearning old ones poorly. You'll end up being more productive in Python than you ever were in Matlab. You'll write idiomatic code.

### How long will it take to learn Python?

[500 hours](https://qr.ae/T3Q1WK). Ok, that number is made up, but it's probably not far from the truth. You can learn the syntax in a weekend. You can make your first significant project in a few days. However, proficiency comes with time. Don't wait until 3 weeks before a technical interview to start learning. I've seen candidates do this, it's not good. You're better off asking for an interview in Matlab if you don't have hundreds of hours of Python under your belt. Start today, keep at it every day (1-2 hours a day will suffice) and it will pay off. 

### Why is Python so popular anyway?

[Yoshua Bengio](https://en.wikipedia.org/wiki/Yoshua_Bengio). Again, I'm halfway joking, but one of the biggest reasons people have moved away from Matlab was the adoption of Python for deep learning. It started with Theano, which came out of Bengio's lab. It built on numpy, scipy, sklearn and jupyter, all of which predated the rise of deep learning. Then came Tensorflow. People at Google were already using Python; Guido von Rossum, creator of Python, was famously employed by Google at one point. Google needed a high-level language to iterate quickly on models; many of the people involved in Theano were involved in Tensorflow. Python made sense. 

It could have landed another way. [We might all be using Lua instead if Yann had prevailed over Yoshua](http://torch.ch/)! But combine industry pressure, lots of money, the education sector needing a good first language, and open source, and Python is a runaway success now. And it might change in the future. Maybe we'll all be using Swift in the future. Or Rust. Or Julia (my personal favorite!). For now, Python is the language to learn.

### I don't even hate Matlab

I've used Matlab extensively. I've been deep enough to create my own mex files and using Java. I've created GUIs in GUIDE. I have created pretty big codebases and classes. I even coded up my own neural net framework which I never published. 

I'm not going to bash Matlab here. You can write good code in Matlab - and many people that have been using Matlab for years end up writing disciplined code. However, I have seen a lot of Matlab code of a certain kind - using matrices for everything (even though Matlab has dataframes and hashmaps!), avoiding for loops (even though it has a great JIT!), using a giant set of globals in GUIDE (there's a way of writing good GUIDE apps, I'm sure!). It will take a little bit of work to unlearn these old habits if you have them. 

### A curriculum

If you have never seen or touched Python, you can start by learning the syntax and the basic data structures (tuples, dicts, and lists) through online resources. 

Some sample websites are:

* [Learn Python](https://www.learnpython.org/). Skip the numpy and pandas tutorials, we'll get back to that later.
* [Codecademy](https://www.codecademy.com/learn/learn-python). Similar.
* [Learn Python The Hard Way](https://learnpythonthehardway.org/python3/). A lot of practical exercises in this one. 30$.
* [Make Art With Python](https://www.makeartwithpython.com/). If you're interested in games and interactive art this might hold your attention. 30$.

Most of these websites will have some sort of live evaluation directly on the website. Pretty soon you'll need a local install of Python. I recommend installing the [Anaconda distribution of Python 3](https://www.anaconda.com/distribution/). This includes the `conda` environment manager, which will allow you to maintain different sets of packages.

### Picking a first project

At this point you could consider using Python for a project (no data science stuff yet). The first app I made was a GUI to upload files to a website. A few years later I made an app in PyQT to annotate physiological recordings with notes. You could make a website. Lots of different projects but basically make sure you cover the basics, meaning:

* functions - these will trip you up. Python has pass-by-reference semantics for object types. In Matlab, a function cannot modify its arguments (unless it's a reference object, but these are pretty uncommon). But in Python you can mess with your arguments:
```python
def my_append_fun(a)
    a.append('b')

c = ['a']
my_append_fun(c)
print(c)
# Prints ['a', 'b']
```
It's not good practice to do this, but you might do it accidentally and you will be very confused.
* modules - in Matlab, one file = one function (unless it's an internal function private to that file). In Python you can have multiple functions and classes inside a file. Each file defines a module that can be imported. Then there's other people's modules! pip! Understanding how and when a certain module or function is accessible is one of the subtle things about Python. 
* tuples, dicts and lists. A simple write-only type for fixed-length groups; a super-powerful hashmap type; and a variable-length vector. It will take you a while to understand the trade-offs for each of these types. Your assumptions will be wrong! You might think appending to a list in a for loop is super slow, because appending to a vector is super slow in Matlab. Wrong! It's actually super fast. 
* classes. Classes are behaviour + data. Maybe you've been doing OOP in Matlab. If not, it's time to pick it up!
* strings and file IO. Format strings, `with` statements, StringIO, regex - all workaday things in a general purpose programming language that you might never have touched in Matlab.

### Data structures and algorithms

Consider learning about data structures and algorithms. Many professional programmers are self-taught and never really learn about these fundamentals. They learn intuitively what is slow and fast, and can code many non-trivial algorithms. They might even use complexity analysis (O notation). 

Once you learn data structures, your world will open up. This is especially true for people with a Matlab background, because the language tends to force you to use the same structure over and over again (the matrix). You might not know what to do with tuples, dicts, lists and objects. You need some solid foundations to transition out of the weird programming model Matlab imposes.

Take the [Algorithms and data structures classes on Coursera by Tim Roughgarden](https://www.coursera.org/specializations/algorithms). These are the same classes you'd get in CS at Stanford, and they are very good. Really tough. You will feel like your mind is melting - in a good way.

You might try a daily challenge, like [hackerrank](https://www.hackerrank.com/). There's [Project Euler](https://projecteuler.net/) if you're more math-inclined. 

### The data science ecosystem

It's finally time learn the data science pipeline. Because you will have learned basic Python well, and the tools are very similar to Matlab, your transition will be very smooth. Here's one tutorial that guides you through the [Python data science ecosystem](https://realpython.com/matlab-vs-python/). This means getting familiarized with:

* matplotlib for plotting
* numpy for matrices
* scipy for signal processing
* pandas for dataframes
* sklearn for machine learning
* jupyter for dynamic notebooks

The hardest package to learn for many people coming from a Matlab background is `pandas`. Why would anyone want to use pandas? *Can't I just use a matrix?* 

How many times has your PhD advisor told you to label your axes in your plots? A thousand times? Labeling axes is important to understand what the data means. When you index into an unlabelled matrix, say `df(:, 7)`, you're giving yourself the possibility of forgetting what the data means. Wouldn't it be better to use `df.reaction_time_ms`? Yes!

You might even have learned how to do reductions, querying and aggregations on raw matrix. This code might give you the mean reaction time for participant 10:

```matlab
mean(df(df(:, 1)==10, 7))
```

That's bad! What it you add a column in your CSV? Then column 7 becomes column 8, your stats are wrong and you'll lose months tracking down the issue. This code is super error-prone and makes kittens cry. I'm not saying it's impossible to do this the right way in Matlab - I'm just saying that's often how people do it. Compare the pandas way: 

```python
df.query('participant_id == 10').reaction_time_ms.mean()
```

[Take the time to read the pandas tutorial in full](https://pandas.pydata.org/pandas-docs/stable/getting_started/10min.html). You might want to pick up a book as well after a little while, for instance [Python for Data Science](https://www.oreilly.com/library/view/python-for-data/9781491957653/). 

 At this point you'll need to practice your new skills. [Join a Kaggle competition](https://www.kaggle.com/), or [follow a data science MOOC](https://www.coursera.org/specializations/jhu-data-science).

### Specialized tools for neuroscience

At this point you might be productive enough to use Python on a daily basis. Congratulations! It's a good time to learn about Python neuroscience tools:

* [nilearn](https://nilearn.github.io/) for machine learning with MRI
* [brian](https://brian2.readthedocs.io/en/stable/) for spiking neural net simulations
* [pytorch](https://pytorch.org/) or [tensorflow](https://www.tensorflow.org/) for fitting ANNs
* [deeplabcut](http://www.mousemotorlab.org/deeplabcut) to track animals without markers
* [Psychopy](https://www.psychopy.org/) for visual stimulus presentation
* [neo](https://github.com/NeuralEnsemble/python-neo) for managing electrophysiology data in Python
* [MNE](https://mne.tools/dev/auto_tutorials/intro/plot_10_overview.html) for EEG analysis
* [PyMC3](https://docs.pymc.io/) for Bayesian inference

Know of another indispensable tool? Write it in the comments.

### Transition existing pipelines to Matlab

It will be hard to transition pipelines developed over years wholesale out of Matlab and into Python. You'll want to freeze data obtained after running a pipeline into a file format that you can transport from Matlab to Python. [Matlab's .mat file format is readable in Python](https://scipy-cookbook.readthedocs.io/items/Reading_mat_files.html). Since v7.3 .mat files are in the hdf5 file format, for which Python has excellent support. 

In the future, you might find that you need Matlab for very little, and only one or two recalcitrant pipelines will need to be maintained. [You could wrap these pipelines in a docker image](https://github.com/mathworks-ref-arch/matlab-dockerfile), so they keep working for years to come, despite changes in OS and Matlab versions.

### Becoming proficient

At this point you might start developing significant codebases. Will you be putting everything in Dropbox? No, you'll be using `git`! You'll need to know the command line. [Follow the software carpentry class](https://software-carpentry.org/lessons/index.html) and learn about the Unix terminal and source control.

To really step up your game, contribute to an open source project. If you're unsure where to start, [join a Brainhack event](https://www.brainhack.org/) - people will ask for volunteers for their projects and they'll guide you through the process of making a submission. Friendships will be created! Collaborations hatched! Bagels will be had! 

Perhaps you'll feel the need for speed at this point. Tear through billion row datasets with [Spark](https://docs.pymc.io/) or [dask](https://dask.org/). JIT your for loops or compile them down to C with [Cython](https://cython.org/), [numba](https://numba.pydata.org/) or [jax](https://github.com/google/jax). [Monte Carlo simulations with a thousand parallel chains](https://rlouf.github.io/post/jax-random-walk-metropolis/)? Not a problem!

### Make it social

People don't realize how social programming is. As a software engineer at Google, I:

* Learned about the core tooling in seminars with other engineers
* Had people review my code
* Reviewed other people's code
* Pair programmed
* Shared analyses with other people who critiqued the analysis (both the content and the method)
* Went to retreats to learn new tools
* Organized a reading group

I learned more from these experiences than from much of the book reading and solitary programming I've done. You don't have to make your learning journey an isolating one. When you do Kaggle, join a team. Go to local meetups - in Montreal for instance, there's [Les Pitonneux](https://www.meetup.com/pitonneux/), who meet up almost daily. Many groups focus on supporting underrepresented groups in computer science, for example [PyLadies](https://www.pyladies.com/).

There are hackerspaces where you might find people in the same situation. You can go to tutorial sessions at conferences. Make friends and create a social support system to help you on your journey. 

### Conclusion

I've had to relearn programming many times over the years. Toolbook, QBasic, VB, Delphi, Actionscript, Perl, PHP - I've written significant chunks of code in each of these languages. They're all either dead or on their way out. Having seen the trajectory of these languages, it feels to me like Matlab is on its way out as well. Which doesn't mean it won't be used at all - after all, PHP is 10 times less popular today than at its peak, but it still runs Facebook! But it does mean that:

* There will be more people who know Matlab than people who are hiring people who know Matlab. It won't do you any favors on your CV.
* Professionals software engineers have already switched away from Matlab. You will have a lot of trouble hiring professional programmers to create Matlab-based infrastructure in your future lab if you choose to stay in academia.
* The Mathworks is a single-source vendor, and their software is closed-source. What happens if they run out of business? 

It's time to move away from Matlab. Take the first step today!