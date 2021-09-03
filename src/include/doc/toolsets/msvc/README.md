# The Hefesto's toolset for MSVC

The way of using it is pretty straightforward. You need to include the main toolset file:

    include ~/toolsets/msvc/msvc.hsl

You have four possible toolsets: msvc-c-app, msvc-c-lib, msvc-cc-app, msvc-cc-lib.

Follows a sample:

    local var src type list;
    local var includes type list;
    local var cflags type list;
    local var libraries type list;
    local var ldflags type list;

    project msvc-lib : toolset "msvc-c-lib" : $src, $includes, $cflags, $libraries, $ldflags, "test.lib";

    msvc-lib.prologue() {
        $src.ls(".*\\.c$");
        $includes = hefesto.sys.get_option("includes");
        $cflags = hefesto.sys.get_option("cflags");
        $libraries = hefesto.sys.get_option("libraries");
        $ldflags = hefesto.sys.get_option("ldflags");
    }

    msvc-lib.epilogue() {
        if (hefesto.sys.last_forge_result() == 0) {
            hefesto.sys.echo("*** done.\n");
        } else {
            hefesto.sys.echo("~~~ error.\n");
        }
    }

This toolset supports the following options:

    - --compile-model=<debug|release> (release is the default)
    - --link-model=<static|shared> (static is the default)
    - --cpu-arch=<x86|x64>
    - --bin-output-dir=<path> (configures the artifact out dir)
    - --charset=<MultiByte|Unicode> (MultiByte is the default)


