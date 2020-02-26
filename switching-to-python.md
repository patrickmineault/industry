# Switching to Python - the missing FAQ

Responses: 

* Time to sit down and put some effort into it
* Navigating workspaces and memory management
   * IDE
   * the 0 index
   * endless options for analysis packages.
* Figuring out how to structure and analyze neural firing
* time course data in python. In matlab, this was all n-dimensional matrices.
*  relearning syntax
* Lack of variable window Which ide? Jupyter seems popular but hard to track variables
* Making nice figures

### How do I get started? I don't have a whole lot of free time

 * Apps on the go
 * software carpentry
 * Hackathon
 
### Which IDE should I use?

* https://www.datacamp.com/community/tutorials/top-python-ides-for-2019
* Two groups: notebooks and text editors
* Jupyter nb/lab/colab is great - literate programming, Binder, etc. Extensions in lab, free stuff in colab. They can get messy. You can run in the cloud.
* Traditional editors - Atom, VSCode (a different product than Visual Studio). Linter support is very useful. An actual text editor is very powerful. Debugging via the debugger.
* People will generally use both - jupyter for notebooks, text editor to develop a package.

### How do I manage memory?

* This is a lot less important in Python than in Matlab
* Tend to have more ephemeral processes: if there's a lot to do, you make a script. Script releases memory once it exists.
* The dominant paradigm for fitting models (PyTorch and TF) implement stochastic gradient descent which means you don't need the data in memory.
* Support for out-of-core computation with dask and spark.
* Jupyter lab can run in the cloud on arbitrarily powerful machines
* Nevertheless:
    * Jupyterlab has an extension.
    * Spyder has a window just for that.
    * You can do it in pure python as well.
    * in ipython and in jupyter, you can use the `%whos` magic command.

### How do you think about 0-indexing and the order of dimensions?

* A: you end to do a lot less of that in Python
* For many types of data, you'll tend to use pandas rather than matrices
* Instead of an array with nans, you'll tend to use a long form pandas dataframe
* If you have temporal data - pandas is the place to start as well
* Easy to reformat your data to deal with nans as well
* There even exists a multidimensional version of xarray

### How do I know which package to use to do X?

* Python has a lot of competing frameworks! That's open source for you.
* Ask around.
* Go to a meetup.
* Use what people are using: on Github, look at number of stars and forks and the data of the last push.

### How do I make nice figures?

* matplotlib makes gross plots by default
* you can make them quite a bit nicer by using the seaborn theme and by increasing the resolution 2-fold (if on a retina display)
* Seaborn has a handful of nice plots and is quite popular.
* My favorites mimic the grammar of graphics (ggplot2 in R)
* https://plotnine.readthedocs.io/en/stable/
* Montreal's own plotly! Datashader!