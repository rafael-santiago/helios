# The Hefesto's C/C++ GCC toolset quick start guide =

The hefesto's C/C++ toolset allows you to compile and link executables and libraries using GCC
compiler.

In order to build an application with hefesto you must use the toolset coded inside "gcc-app.hsl" file,
located under "toolsets/gcc/gcc-app.hsl".

The first thing to do is to include this important file in your Forgefile, in the following way:

    include ~/toolsets/gcc/gcc-app.hsl

After, you can declare your project:

    var mydeps type string;
    var source_list type list;
    var includes_dirs type list;
    var compiler_options type list;
    var libraries_dirs type list;
    var linker_flags type list;
    var appname type string;

    project myprojname : toolset "gcc-c-app" : dependencies $mydeps :
        $source_list, $includes_dirs, $compiler_options, $libraries_dirs, $linker_flags, $appname ;

The presented example is using the "gcc-c-app" toolset, destinated to build C executables, if you need
to build C++ executables use the "gcc-cc-app".

The toolset's forge function receives:

    - a list containing all project's implementation files.
    - a list containing extra includes' directories.
    - a list containing yours desired compiler options.
    - a list containing extra libraries' directories.
    - a list containing yours desired linker options.
    - a string specifing the application name.

You can use the compiler model in "debug" or "release" with command option "--compile-model=release|debug", the
default is "release".

You can also change the link model, using the command option "--link-model=shared|static", the default is
"shared".

If you need to force the compilation of all project source files, use the command option "--forge-anyway".

The toolsets used to compile/link libraries works in the same described way.

In order to specify where to generate the object file use the option "--obj-output-dir=<path>".

Also it is possible to specify the output directory for the binary using the option "--bin-output-dir=<path>".

The toolset used to link static/shared libraries is named "gcc-c-lib" for C language and "gcc-cc-lib" for
C++ language... And it is located under "toolsets/gcc/gcc-lib.hsl".

If you want scan dependencies instead of hardcode it, you can use the dependency scanner located in
"toolsets/common/utils/lang/c/dependency_scanner.hsl", the usage is fairly simple:

    include ~/toolsets/gcc/gcc-app.hsl
    include ~/toolsets/common/utils/lang/c/dependency_scanner.hsl

    var mydeps type string;
    var source_list type list;
    var includes_dirs type list;
    var compiler_options type list;
    var libraries_dirs type list;
    var linker_flags type list;
    var appname type string;

    project myprojname : toolset "gcc-c-app" : dependencies $mydeps :
        $source_list, $includes_dirs, $compiler_options, $libraries_dirs, $linker_flags, $appname ;


    myprojname.prologue() {
        # insted of hardcode it... scan.
        $mydeps = get_project_dependencies();
    }

Some forge invocation examples:

    * An application that uses posix threads in release/shared models [default compile/link models]

        hefesto --forgefiles=myprojname.hsl --myprojname-projects=myprojname --ldflags=-lpthread

    * An application that uses posix threads in debug/shared models

        hefesto --forgefiles=myprojname.hsl --myprojname-projects=myprojname --compile-model=debug --ldflags=-lpthread

    * An application that uses posix threads in release/static models

        hefesto --forgefiles=myprojname.hsl --myprojname-projects=myprojname --link-model=static --ldflags=-lpthread

    * An application that uses posix threads in debug/static models

        hefesto --forgefiles=myprojname.hsl --myprojname-projects=myprojname --compile-model=debug --link-model=static --ldflags=-lpthread

    * An application that uses posix threads, math lib and some foo static lib

        hefesto --forgefiles=myprojname.hsl --myprojname-projects=myprojname --ldflags=-lpthread,-lm,../res/foo/foo.a
