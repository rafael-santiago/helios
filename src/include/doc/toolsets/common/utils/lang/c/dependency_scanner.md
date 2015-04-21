# The dependency_scanner.hsl module

This module brings a ``HSL`` function which can make ``dep-chains`` for *C/C++*.

## Default location of this module

>``include ~/toolsets/common/utils/lang/c/dependency_scanner.hsl``

## The ``get_c_cpp_deps()`` function

This function results a ``dep-chain`` based on *C/C++* headers and implementation files present in the current working directory.

>``$dep_chain = get_c_cpp_deps()``

If there are more files in another subdirectory, you should try:

>``hefesto.sys.cd("another-one-directory");``
>
>``$dep_chain = $dep_chain + get_c_cpp_deps();``
>
>``hefesto.sys.cd("..");``
