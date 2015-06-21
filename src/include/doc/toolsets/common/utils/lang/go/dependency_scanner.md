# The dependency_scanner.hsl module

This module brings a ``HSL`` function which can make ``dep-chains`` for *Go*.

## Default location of this module

>``include ~/toolsets/common/utils/lang/go/dependency_scanner.hsl``

## The ``get_go_deps()`` function

This function results a ``dep-chain`` based on *Go* imports done in the existent files from the current working directory.

>``$dep_chain = get_go_deps()``

If there are more files in another subdirectory, you should try:

>``hefesto.sys.cd("another-one-directory");``
>
>``$dep_chain = $dep_chain + get_go_deps();``
>
>``hefesto.sys.cd("..");``

However, if you have this following directory layout for your golang project:

        /proj/src/
                 /pkg0
                 /pkg1
                 /pkgn
                 /main.go

and inside the file ``main.go`` you defined these imports:

        import (
                  "./pkg0"
                  "./pkg1"
                  "./pkgn"
        )

Now, supposing that you call ``get_go_deps()`` being inside ``/proj/src``. The dependencies
inside the ``local packages`` will be detected by this call by default. You do not have to
switch to these packages subdirectories in order to scan their dependencies. Being it
automatically scanned by the ``get_go_deps()`` function.
