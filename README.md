Aya: Run a command remotely with local data
===========================================

Aya is used to sync a directory tree to a remote machine and run a
command on the remote machine within the copied directory tree.

Usage
-----

Create a file called .aya in the root of the directory tree you wish
to copy to the remote machine. If the .aya file is nonempty, it should
contain a list of filename globs, one per line, indicating which files
*should not* be copied to the remote machine.

To execute a command remotely within a directory tree containing .aya
file in its root, run

    aya [username@]host:path command

Example
-------

Suppose we have a project rooted at /home/user/proj; we wish to copy
/home/user/proj to beefymachine:/tmp/proj and run
src/regressiontest.py on beefymachine. To make the data transfer go
faster, we'll avoid copying any object files.

First, create the file /home/user/proj/.aya:

    *.o

Then, in /home/user/proj/src/, execute

    aya beefymachine:/tmp/proj ./regressiontest.py

Aya will copy all the files in /home/user/proj, except any files
ending in .o, to the directory /tmp/proj on beefymachine and execute
tmp/src/regressiontest.py on beefymachine in the working directory
tmp/src.

Aya uses rsync to do the copying so that repeated executions should
be quite fast if little data have changed.
