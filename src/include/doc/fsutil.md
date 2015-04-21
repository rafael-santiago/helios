# The fsutil.hsl module

This module brings a set of ``HSL`` functions for common filesystem operations.

## Default location of this module

>``include ~/fsutil.hsl``

## The ``filenamewnoext()`` function

This function results the passed file name without its extension.

>``$only_the_name = filenamewnoext("fsutil.md");``

## The ``pathfromfilepath()`` function

This function results only the path of a passed file path.

>``$only_the_path = pathfromfilepath("/usr/local/share/hefesto/includes/fsutil.md");``

## The ``filenamefrompath()`` function

This function results only the filename from a file path.

>``$only_the_filename = filenamefrompath($fullpath);``

## The ``isdir()`` function

This function verifies if a passed path is a directory or not, being a directory it results *1* otherwise *0*.

>``if (isdir($path)) hefesto.sys.echo($path + " is a directory.\n");``

## The ``isfile()`` function

This function verifies if a passed path is a regular file (which not includes a directory) or not, being a regular file it results *1* otherwise *0*.

>``if (isfile($path)) hefesto.sys.rm($path);``

## The ``mktree()`` function

This function creates the necessary elements to compose the passed directory path. On success it results *1* otherwise *0*.

>``if (mktree($path)) hefesto.sys.echo("The path was successfully created.\n");``

## The ``rmtree()`` function

This function removes an empty directory tree. On success it results *1* otherwise *0*.

>``if (rmtree($path)) hefesto.sys.echo("All cleaned.\n");``

## The ``lsdir()`` function

This function results list containing all current subdirectories present in the ``cwd``.

>``$subdirs = lsdir();``

