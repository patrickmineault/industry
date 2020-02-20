## Transitioning away from Matlab

I mentioned in my last article on getting a job in industry that I had been programming Python on and off for 10 years when I got my first non-academic job. Having proficiency in a language that people use outside of academia will improve your chances of getting a job in industry. But what if you're in a lab that's been using Matlab for years and you haven't had a chance to learn Python? Here's my guide to transition off of Matlab to Python.

### Learn Python the hard way

Python is one of the most popular languages out there - more popular than Matlab by a factor of at least 10 - and it's the language the vast majority people transitioning from Matlab will choose. There's two basic strategies you can apply here:

* Transfer learning (aka the easy way). You have things in Matlab you use every day - array operations, plotting, signal processing, etc. Learn to do the same thing in Python. A lot of the Python data science API (numpy, scipy and matplotlib in particular) are very very similar to Matlab (often because they were originally built to replicate functionality in Matlab). With this route you'll get moderately productive very fast. 
* Starting from scratch (aka the hard way). Learn the syntax, then do something you couldn't do in Matlab, for example:
  * Learn algorithms and data structures
  * Make a GUI application (e.g. in PyQT)
  * Make a game
  * Make a dynamic website

My (slightly controversial) opinion is you're better off starting from scratch. If you use the transfer learning method you will, for a long time, be less productive than you currently are. You will feel annoyed at your own incompetence (*"why am I doing this? I could do the same thing twice as fast!"*). Furthermore, you will have a tendency of doing things *the Matlab way* (using matrices for everything, index chaining, avoiding for loops) that are error-prone and you shouldn't be doing in a general purpose programming language. 

By starting from scratch you will learn new things you could not do before at all - you will feel like you have new powers. You can write a GUI! You can make dynamic visualizations! You can make games! You can do deep learning! Your day-to-day productivity won't suffer if you're using Matlab for *real work* for a while. Then when it's time to hit the switch, boom! You'll end up being more productive in Python than you ever were in Matlab. You'll write idiomatic code.

### How long will it take to learn Python?

[500 hours](https://qr.ae/T3Q1WK). Ok, that number is made up, but it's probably not far from the truth. You can learn the syntax in a weekend. You can make your first significant project in a few days. However, proficiency comes with time. Don't wait until 3 weeks before a technical interview to start learning (I've seen candidates do this, it's not good). Start today, keep at it every day (1 hour a day will suffice) and it will pay off. 

### A curriculum

If you have never seen or touched Python, you can start by learning the syntax and the basic data structures (tuples, dicts, and lists) through online resources. Some you will have to pay for, others not. 30$ is not much for a lifelong skill.

Some sample websites are:

* [Learn Python](https://www.learnpython.org/). Skip the numpy and pandas tutorials, we'll get back to that later.
* [Codecademy](https://www.codecademy.com/learn/learn-python). Similar.
* [Learn Python The Hard Way](https://learnpythonthehardway.org/python3/). A lot of practical exercises in this one.
* [Make Art With Python](https://www.makeartwithpython.com/). If you're interested in games and interactive art this might hold your attention.

Most of these websites will have some sort of live evaluation directly on the website. Pretty soon you'll need a local install of Python. These days, most tutorials recommend installing the [Anaconda distribution of Python 3](https://www.anaconda.com/distribution/). This includes the `conda` environment manager, which will allow you to maintain different sets of packages.

At this point you could consider using Python for a project (no data science stuff yet). The first app I made was a GUI to upload files to a website. A few years later I made an app in PyQT to annotate physiological recordings with notes. You could make a website. Lots of different projects but basically make sure you get to use the basics, meaning:

* functions
* modules
* tuples, dicts and lists
* classes
* strings
* file IO

Then consider learning about data structures and algorithms. If you've used Matlab for a while you might have an intuitive understanding of what is slow or fast. You've likely coded up many non-trivial algorithms, of your own design or things that you've seen in papers. You might even have used complexity analysis (O notation). But you generally you will have used one data structure over and over again (the matrix) and you might not know what to do with tuples, dicts, lists and objects. 

### Becoming stronger

Take the [Algorithms and data structures classes on Coursera by Tim Roughgarden](https://www.coursera.org/specializations/algorithms). These are the same classes you'd get in CS at Stanford, and they are very very good. Really tough. You will feel like your mind is melting (in a good way).

You might want to try a daily challenge. Some recommend [hackerrank](https://www.hackerrank.com/). There's [Project Euler](https://projecteuler.net/) if you're more math-inclined. 

Then it's time to finally learn the data science pipeline. Because you will have learned basic Python well, and the tools are very similar to Matlab, your transition will be really smooth. Here's one tutorial that guides you through the [Python data science ecosystem](https://realpython.com/matlab-vs-python/). This means getting familiarized with:

* matplotlib
* numpy
* scipy
* pandas
* sklearn
* jupyter

At this point you'll need to practice these new found skills. [Join a Kaggle competition](https://www.kaggle.com/), or [follow a data science MOOC](https://www.coursera.org/specializations/jhu-data-science).

### Specialized tools

At this point you might be productive enough to use Python on a daily basis. Congratulations! It's a good time to learn about Python neuroscience tools:

* [nilearn](https://nilearn.github.io/) for machine learning for MRI
* [brian](https://brian2.readthedocs.io/en/stable/) for spiking neural net simulations
* [pytorch](https://pytorch.org/) or [tensorflow](https://www.tensorflow.org/) for fitting ANNs
* [deeplabcut](http://www.mousemotorlab.org/deeplabcut) to track animals without markers
* [Psychopy](https://www.psychopy.org/) for visual stimulus presentation

This is just a sampling but there are many tools available for neuro.

### Becoming proficient

At this point you might start developing significant codebases. Will you be putting everything in Dropbox? Of course not, you'll be using `git`. You'll need to know the command line to be use it to its optimum. [Follow the software carpentry class](https://software-carpentry.org/lessons/index.html).

The thing that will really make you step up your game is contributing to an open source project. If you're unsure where to start, [join a Brainhack event](https://www.brainhack.org/) - people will ask for volunteers for their projects and they'll guide you through the process of making a submission. Bagels will be had.

### Make it social

People don't realize how social programming is. As a software enginner at Google, I:

* Learned about the core tooling in seminars with other engineers
* Had people review my code
* Reviewed other people's code
* Pair programmed
* Shared analyses with other people
* Went to retreats to learn new tools
* Organized a reading group

I learned more from these experiences than from much of the book reading and solitary programming I've done. You don't have to make your learning journey an isolating one. When you do Kaggle, join a team. Go to local meetups. Organize or join hackathons. Go to tutorial sessions at conferences. Make friends and create a social support system to help you on your journey. 

Take the first step today!