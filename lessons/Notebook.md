# Jupyter notebooks

This lesson will show you the basics of working with Jupyter notebooks
(previously known as IPython notebooks). First let's start by launching the
notebook. If you are using anaconda, just click on the launch Notebook icon
or on a terminal type:

```
$ jupyter notebook
```

This should cause a new browser window to open or open new tab in already
opened web browser, showing the notebook Dashboard. On this screen, click
on: `New > Python 3`, to start a new notebook. You can change the title of
the notebook to anything you like.

## Notebook basics

A Notebook is an interactive execution environment, in this case for Python 3.
The main idea is that we have a *kernel*, which is running in the background,
and we interact with this kernel via the browser. (Kernels for other languages
are available).

We send instructions to the kernel by executing *cells*, and we get the
response from the kernel as the output of our cell.

```
1 + 1
```

Notice that variables (data) remain loaded in our kernel, until we shut it down.
This means that we can define a variable in one cell, and use it in another.

This is a cell. In a cell we enter code:
```
a = 1 + 1
```

```
print(a)
```

Cell has an `In [ ]:` *prompt* next to it. Once we execute cell, we have a
`In [n]:` prompt, where `n*`is the execution number of the cell -- this way we
know in which order we have run things. A cell has also a `Out [n]:` prompt,
which indicates the result of the cell.

## Notebook user interface

There are several ways to run code in a cell:
 - Selecting from the menu Cell > Run
 - **Ctrl + enter (run and keep same cell selected)**
 - Shift + enter (run and move to cell below)
 - Alt + enter (run and insert new cell below)

Obviously, we need to add more cells to be able to continue working. You can
also re-order cells if you want.

## Tool bar
Let's walk through the options in the tool bar.

 - The `Save` icon saves the notebook. Notice that notebooks also get autosaved
   periodically.
 - **+** inserts a new cell
 - Cut, copy and paste cells
 - Up/down arrows to reorganize cells
 - Run/stop cell from running
   - Stop some slow running code, for example:
    ```
    import time
    time.sleep(10)
    print('If you can see this message, your cell has finished running')
    ```
 - Select cell type

## Cell types
There are three different kinds of cells:

 - Code cells - the type of cell we've used above, (in and out)
 - Markdown - in these cells we can write text using the
  [Markdown language](http://jupyter.cs.brynmawr.edu/hub/dblank/public/Jupyter%20Notebook%20Users%20Manual.ipynb#4.-Using-Markdown-Cells-for-Writing).
 - Raw cell - these cells are just plain text, which does not get processed in any way.

## Markdown cells
In a nutshell, Markdown allows us to create:
 - Lists
  - with sub items
    1. and numbering
 - *italic* and **bold** text
 - LaTeX:
```
$$
{\cal N}(\mu, \sigma^2) = \frac{1}{\sigma\sqrt{2\pi}} e^{-\frac{(x-\mu)^2}{2\sigma^2}}
$$
```

## More on code cells
In addition to *normal* Python, we can use code cells to run *magic functions*.
These magic functions allow us to execute commands which are not strictly
speaking Python:

 - Bash commands (use `!` prefix) (such as `!ls` or `!pwd`)
 - ``%%timeit`
 - `%pylab inline` (nice for plotting)

## Other nice features

 - tab to auto complete (e.g. `np.lin + tab`)
 - inline documentation (e.g. `np.linspace + Shift + tab` 1x-4x)
 - Prefix with `?` to show documentation (e.g. `?np.linspace`)
 - Prefix with `??` to show code (e.g. `??np.linspace`)
 - Plays nice with Pandas

## References
 - http://nbviewer.jupyter.org/github/jupyter/notebook/blob/master/docs/source/examples/Notebook/Examples%20and%20Tutorials%20Index.ipynb
