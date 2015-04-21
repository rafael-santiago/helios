# The diff.hsl module

This module brings a ``HSL`` function to diff evaluation between to files.

## Default location of this module

>``include ~/diff.hsl``

## The ``diff()`` function

This function verifies if the two passed path files differs or not. If there is some difference between them the function results *1* otherwise *0*.

>``if (diff("/home/you/temp.file", "~/temp.file")) hefesto.sys.echo("You are not you.\n");``
