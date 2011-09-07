Aya: Run a command remotely with local data
===========================================

Aya is used to copy a directory tree to a remote machine and run a
command on the remote machine within the copied directory tree.

This is useful when the time spent copying the data to the remote
machine is dwarfed by the time saved by running on a more powerful
machine; for example, I use it to run regression tests on my work
desktop while programming on my personal laptop.

Usage
-----

Create a file called .aya in the root of the directory tree you wish
to copy to the remote machine. If the .aya file is nonempty, it should
contain a list of filename globs, one per line, indicating which files
*should not* be copied to the remote machine.

To execute a command remotely within a directory tree containing .aya
file in its root, run

    aya [host] [command]

Example
-------

Suppose we have a project rooted at /home/user/proj; we wish to copy
/home/user/proj to beefymachine and run src/regressiontest.py on
beefymachine. To make the data transfer go faster, we'll avoid copying
any object files.

First, create the file /home/user/proj/.aya:

    *.o

Then, in /home/user/proj/src/, execute

    aya beefymachine ./regressiontest.py

Aya will copy all the files in /home/user/proj, except any files
ending in .o, to a temporary directory tmp on beefymachine and execute
tmp/src/regressiontest.py on beefymachine in the working directory
tmp/src.
