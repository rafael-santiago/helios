# The sysinfo.hsl module

This module brings a ``HSL`` functions for system information acquiring.

## Default location of this module

>``include ~/sysinfo.hsl``

## The ``sysinfo_is64()`` function

This function results *1* when the current system is 64-bit otherwise *0*.

>``if (sysinfo_is64()) hefesto.sys.echo("64-bit stuff goes here...\n");``

## The ``sysinfo_cpu_wsize()`` function

This function results the ``word-size`` of the current ``cpu``.

>``if (sysinfo_cpu_wsize() == 32) hefesto.sys.echo("32-bit stuff goes here...\n");``
