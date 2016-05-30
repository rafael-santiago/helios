# The dependency_scanner.hsl module

This module brings a ``HSL`` function which can make ``dep-chains`` for *C/C++*.

## Default location of this module

>``include ~/toolsets/common/utils/lang/c/dependency_scanner.hsl``

## The ``get_c_cpp_deps()`` function

This function results a ``dep-chain`` based on *C/C++* headers and implementation files present in the current working directory.

>``$dep_chain = get_c_cpp_deps()``

If there are more files in another sub-directory, you should try:

>``hefesto.sys.cd("another-one-directory");``
>
>``$dep_chain = $dep_chain + get_c_cpp_deps();``
>
>``hefesto.sys.cd("..");``

Sometimes, seeking to be tidy, people separate the source code inside specifics sub-directories. In this case you should
set the evironment variable ``GET_C_CPP_DEPS_SRC_ROOT`` to the lowest path where all your code is contained. Supposing
that you have the following project ``src-tree``:

        project/
            src/
                memory/
                boot/
                filesystem/
                process/
                etc/

For the previous showed project's ``src-tree`` you should the following before traversing all sub-directories calling
``get_c_cpp_deps()`` once per each one.

>``hefesto.sys.env("GET_C_CPP_DEPS_SRC_ROOT", hefesto.sys.pwd());``

The code above will allow the dependency scanner find an ``C/C++ file`` defined in a specific sub-directory being
inside other one.
