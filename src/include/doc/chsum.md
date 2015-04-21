# The chsum.hsl module

This module brings a ``HSL`` function which evaluates the checksum based on the two complement of one.

## Default location of this module

>``include ~/chsum.hsl``

## The function ``eval_buffer_chsum()``

This function evaluates and results the checksum of a passed string buffer. The first argument is the previous checksum evaluation, if it is being still generated must be zero.

>``$buffer_checksum = eval_buffer_chsum(0, $buffer);``

In order to check the buffer integrity it is necessary verify the ``eval_buffer_chsum()`` result. If *0* it means ok otherwise the buffer is dirty in some way.

>``if (eval_buffer_chsum($previous_chsum, $buffer) != 0) hefesto.sys.echo("Integrity check error!\n");``
