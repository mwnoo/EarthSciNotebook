# IPython

Assorted notes on using the ipython interactive shell. Official
documentation is at <http://ipython.org>.

 **See also:** [General programming](programming.md), [Python notes](python_notes.md) pages.

## Basics

* **Pylab** - Starting ipython with the `--pylab` option imports
        numpy and matplotlib libraries into the workspace.

* **Inline help** - Following any object of function name with a
        "?" gives info or documentation about the item.

* **Shell access** - to run a command in the system shell prefix
        it with an exclamation point: `!ping www.bbc.co.uk`

* **ipdb** - ipython has an enhanced debugger (not sure if this is
        enabled by default :!:)

## Magic commands

IPython "magic" commands operate only within IPython, and are prefaced
by %. If the flag %automagic is set, then magic commands can be called
without the %. (%automagic is on by default.). These commands include:

* Functions that work with code: %run, %edit, %save, %macro, %recall, etc.
* Functions which affect the shell: %colors, %xmode, %autoindent, etc.
* Other functions such as %reset, %timeit or %paste.
* To see all the available magic functions, call %lsmagic.
* [This](http://ipython.org/ipython-doc/stable/api/generated/IPython.core.magic.html#module-IPython.core.magic)lists all the core magic functions.`

### %run

Run any python script and load all of its data directly into the
interactive namespace. Since the file is re-read from disk each time,
changes you make to it are reflected immediately (unlike imported
modules, which have to be specifically reloaded). %run has special flags
for timing the execution of your scripts (-t), or for running them under
the control of either Python’s pdb debugger (-d) or profiler (-p).

You can step through a program from the beginning by calling `%run -d
theprogram.py`

### %who, %whos

Print all interactive variables, with minimal (%who) or extensive
(%whos) formatting. If any arguments are given, only variables whose
type matches one of these are printed. For example:

~~~
#This will list functions and strings, excluding all other types of variables
%who function str
~~~

### %edit

Gives a reasonable approximation of multiline editing, by invoking your
favorite editor on the spot. IPython will execute the code you type in
there as if it were typed interactively.

### %debug, %pdb, %prun

After an exception occurs, you can call `%debug` to jump into the Python
debugger (pdb) and examine the problem. Alternatively, if you call `%pdb`,
IPython will automatically start the debugger on any uncaught exception.
`%prun` will run a statement through the python code profiler.



