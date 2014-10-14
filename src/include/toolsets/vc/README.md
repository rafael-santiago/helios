# The Hefesto's Vc-100/110 toolset start guide

With hefesto's vc-100/110 toolset you can build executables and libraries using Visual C compiler from Visual Studio 10/11.

The first thing to do is include the main hsl file related with this toolset.

To executables you must use:

    include ~/toolsets/vc/vc110-app.hsl

To libraries you must use:

    include ~/toolsets/vc/vc110-lib.hsl

Both toolsets receive five lists and one string as arguments.

The first list must contain all file's paths (from files that will be compiled).

The second list must contain all extra includes paths.

The third list must contain all compilation options which will be passed to the compiler.

The fourth list must contain all extra libs paths.

The fifth list must contain all linker options which will be passed to the linker.

The string is the output name for your exe or lib.

Follows all it coded:

    # "hello-world.hsl"

    include ~/toolsets/vc/vc110-app.hsl

    var sources type list;
    var includes type list;
    var libpaths type list;
    var ldflags type list;
    var cflags type list;

    project hello-world : toolset "vc110-app" :
        $sources,
        $includes,
        $cflags,
        $libpaths,
        $ldflags,
        "hello.exe" ;

    hello-world.prologue() {
        $includes = hefesto.sys.get_option("includes"); # populating the includes list from user's cmdline option.
        $cflags = hefesto.sys.get_option("cflags"); # idem with cflags list.
        $libpaths = hefesto.sys.get_option("libs"); # idem with libpaths list.
        $ldflags = hefesto.sys.get_option("ldflags"); # idem with ldflags list.
        $sources.set_from_fs_by_regex("\\.c$"); # adding all .c from current directory, these files will be compiled.
    }

You can build applications and libraries in release/debug compilation model and still in shared/static linkage.

The option --compile-model specifies the compilation model (debug | release [the default]).

The option --link-model specifies the link model (shared | static [the default]).

The option --mk-pdb requests the creation of pdb files when compilation model is "release".

Some examples:

    hefesto --forgefiles=hello-world.hsl --hello-world-projects=hello-world

    hefesto --forgefiles=hello-world.hsl --hello-world-projects=hello-world --compile-model=debug

    hefesto --forgefiles=hello-world.hsl --hello-world-projects=hello-world --mk-pdb --ldflags=res\\bla.lib,res\\blanet.lib,wsock32.lib --includes=additional\\includes\\bla\\,additional\\includes\\blanet

