# The lsutil.hsl module

This module brings a ``HSL`` functions for list handling.

## Default location of this module

>``include ~/lsutil.hsl``

## The ``lsdup()`` function

This function results a copy of the passed list.

>``$list_copy = lsdup($original_list);``

## The ``ls2str()`` function

This function results a string representation of the passed list with new-line symbol as item separator.

>``$list_str = ls2str($list_copy);``
