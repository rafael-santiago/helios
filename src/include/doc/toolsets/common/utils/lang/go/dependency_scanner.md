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
