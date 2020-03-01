
### How do I get started? I don't have a whole lot of free time

 * Apps on the go
 * software carpentry
 * Hackathon
 
### Which IDE should I use?

Feature | PyCharm | JupyterLab | Spyder | Atom/Hydrogen 
--- | --- | --- | --- | --- 
Live code analysis | yes | no | yes | yes
Autocomplete | `Ctrl+Space` | `Tab` | `Ctrl+Space` or `Tab` | `Tab`
Debugger support | yes | [with extension](https://github.com/jupyterlab/debugger) | yes | yes 
Command palette |  `Ctrl+Shift+A` | `Ctrl+Shift+C` | - | `Ctrl+Shift+P`
Define cell | `#%%` | `+`, `b`, `a` | `#%%` | `#%%`
List variables | panel | `%whos` magic or [extension](https://github.com/lckr/jupyterlab-variableInspector) | panel | `%whos` magic, watches
High-DPI support (retina display) | good | good | ok | good
Dark theme | yes | yes | partial | yes
Code refactoring | yes | no | no | yes
Markdown preview | yes | yes | no | yes
Other languages besides Python | yes | yes | not really | yes
Userbase | ? | [2M+ notebooks on Github, 9400 stars](https://blog.jupyter.org/jupyterlab-is-ready-for-users-5a6f039b8906) | [5200 stars on Github](https://github.com/spyder-ide/spyder) | [1.6M installs, 700 stars](https://atom.io/packages/hydrogen)
Cost | 89$/year | free | free | free
Hero feature | Built like a tank | Run anywhere, Binder | Lightweight, batteries included | Mix notebooks and scripts 

Hot takes:

## Atom

* not having a console to look at is annoying. Would prefer a Spyder-type setup.

## 
* PyCharm: Will do a lot for you. Will auto-add imports, fill in requirements.txt. Encourages you to be structured.
* The debugger has an inline tracer which is incredible

* https://www.datacamp.com/community/tutorials/top-python-ides-for-2019
* Two groups: notebooks and text editors
* Jupyter nb/lab/colab is great - literate programming, Binder, etc. Extensions in lab, free stuff in colab. They can get messy. You can run in the cloud.
* Traditional editors - Atom, VSCode (a different product than Visual Studio). Linter support is very useful. An actual text editor is very powerful. Debugging via the debugger.
* People will generally use both - jupyter for notebooks, text editor to develop a package.

One issue with JupyterLab is that nonlinear code execution can create code that is irreproducible and hard to reason about. There are ways to avoid these issues, like separating out the largest pieces of code into their own modules. This can bring its own difficulties; when Python imports a module, it creates a snapshot of this module at that point in time. When you change the code of the underlying module, you have to explicitly reload the module using the `reload` command or your changes will be ignored. [You can use the `%autoreload` magic to avoid this](https://blog.godatadriven.com/write-less-terrible-notebook-code).  

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

### Figuring out how to structure and analyze neural firing time course data in python. In matlab, this was all n-dimensional matrices.
