# PyQt5

We can create a design in the designer, then save the `.ui` file. When we want to actually use this file with some python code, we have to run the `pyuic5` command.

Let's say we have a ui file called `mainwindow.ui`. We run `pyuic5 -x mainwindow.ui -o mainwindow.py`.

The parameter after the `-o` is the name of the output python file we want to generate.

Now when we run `python mainwindow.py` we see the screen we just created.
