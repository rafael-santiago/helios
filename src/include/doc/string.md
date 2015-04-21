# The string.hsl module

This module brings a set of ``HSL`` functions for string handling.

## Default location of this module

>``include ~/string.hsl``

Follows a short description of each one.

## The ``reverse_string()`` function

This function reverses a string sequence resulting the reverse of this.

>``$strrev = reverse_string("SOCORRAM ME SUBI NUM ONIBUS EM MARROCOS");``

## The ``split_string()`` function

This function splits a string sequence based on a supplied token resulting a list of this.

>``$my_serialized_str = split_string("a, b, c,d,e", ",");``

## The ``make_string()`` function

This function makes a string based on a supplied list and string token. It results a string.

>``$my_unserialized_list = make_string($alpha_list, ",");``

## The ``strlwr()`` function

This function results the lower-case version of a passed string.

>``$all_lower = strlwr("NoRmAl");``

## The ``strupr()`` function

This function results the upper-case version of a passed string.

>``$all_upper = strupr("nOrMaL");``

## The ``ltrim()`` function

This function results the passed string without left trailing blanks.

>``$no_blanks_L = ltrim("     boo!");``

## The ``rtrim()`` function

This function results the passed string without right trailing blanks.

>``$no_blanks_R = rtrim("boo!    ");``

## The ``trim()`` function

This function results the passed string without left, right or middle trailing blanks.

>``$no_blanks_at_all = trim("  b  o  o  !  ");``

## The ``strpos()`` function

This function results the start index of the passed substring into the passed string.

>``$start_index = strpos("There is a neddle in the haystack", "needle");``
