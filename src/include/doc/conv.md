# The conv.hsl module

This module brings a ``HSL`` functions for conversion handling and related things.

## Default location of this module

>``include ~/conv.hsl``

## The ``isxdigit()`` function

This function verifies if the passed symbol is a hexadecimal digit or not. Resulting *1* when it is and *0* when not.

>``if (isxdigit($curr_dig)) hefesto.sys.echo("Do some hexadecimal stuff here...\n");``

## The ``int2hex()`` function

This function results the passed ``32-bit`` number in its hexadecimal notation.

>``$str_hex = int2hex("1982");``

## The ``isdigit()`` function

This function results *1* when the passed symbols is a decimal number otherwise *0*.

>``if (isdigit($curr_dig)) hefesto.sys.echo("Do some decimal stuff here...\n");``

## The ``isdecimal()`` function

This function results *1* when the passed string represents a valid decimal number otherwise *0*.

>``if (isdecimal("-49")) hefesto.sys.echo("Valid decimal...\n");``

## The ``ishex()`` function

This function results *1* when the passed string represents a valid hexadecimal number otherwise *0*.

>``if (ishex("DeaDBeeF")) hefesto.sys.echo("Valid hexadecimal...\n");``

## The ``xnib2int()`` function

This function results the value of the passed nibble.

>``$hex_value = ($hex_value << 4) | xnib2int($nibble);``

## The ``hex2int()`` function

This function results the decimal value of the passed hexadecimal number.

>``$value = hex2int("deadbeef");``

## The ``str2int()`` function

This function results the decimal value of a passed string containing a decimal value.

>``$value = str2int("-1092");``

