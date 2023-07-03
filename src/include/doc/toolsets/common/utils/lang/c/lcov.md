# The LCOV generator

This is a convenience wrapper for LCOV usage. It works with GCC or
Clang and it is also able to detect which of those compilers are
in use when called generate_lcov_report() function.

There is no secret on using it, once your code compiled with --coverage
option and your code ran, all you should do is call generate_lcov_report()
function passing the object output directory.

If your entry point is in a file different of main.c you must pass the
full qualified path of it through the option --main-obj-filepath=<path>

If your application when execute generates gcda file in several directories
you must pass those path in --gcda-search-path=<path0>,...,<pathN> option.

If you want to generate the coverage info file in a directory different
from the --obj-output-dir option, you must use the option
--lcov-filepath=<path> option. It defaults to 'coverage.info'.

If there are patterns that should be removed from lcov report, you
must use the option --lcov-remove-patterns=<pattern0>,...,<patternN>
option.

If you want to generate the HTML based report you must use
--genhtml-outpath=<directory path> option. It creates the path
if it does not exist.

You can pass the genhtml's rendering options through the option
--genhtml-rendering-options=<option0>,...,<optionN>

Example:

```
# Forgefile.hsl
include ~/toolsets/gcc/gcc-app.hsl
include ~/toolsets/common/utils/lang/c/dependency_scanner.hsl
include ~/toolsets/common/utils/lang/c/lcov.hsl

local var sources type list;
local var includes type list;
local var cflags type list;
local var libraries type list;
local var ldflags type list;
local var deps type string;

project coverage : toolset "gcc-c-app" :
        dependencies $deps : $sources, $includes, $cflags,
                             $libraries, $ldflags, "coverage";

coverage.prologue() {
    $deps = get_c_cpp_deps();
    $sources.ls(".*\\.c$");
}

coverage.epilogue() {
    hefesto.sys.run("bin/coverage");
    var option type list;
    var obj_output_dir type string;
    $option = hefesto.sys.option("obj-output-dir");
    if ($option.count() > 0) {
        $obj_output_dir = $option.item(0);
    } else {
        $obj_output_dir = hefesto.sys.pwd();
    }
    if (generate_lcov_report($obj_output_dir) != 0) {
        hefesto.project.abort(1);
    }
    if (hefesto.sys.last_forge_result() == 0) {
        hefesto.sys.echo("Done!\n");
    }
}
```

`.ivk` file:

```
--forgefiles=Forgefile.hsl --Forgefile-projects=coverage --obj-output-dir=o --bin-output-dir=bin
```

Forge invocation example:

```
_ hefesto --coverage --genhtml-rendering-options=--legend --genhtml-outpath=reports/coverage
```
