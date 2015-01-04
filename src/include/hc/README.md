# The Hefesto check functions

Hefesto check functions is a collection of HSL codes destinated to verify if a build environment
has all requirements needed to run a forge task. Things like look for some software exportation,
library installation, library versioning, software versioning and so on.

All functions of this collection have names prefixed by "hc_" and are int/boolean functions which
means return 1 for ok results otherwise 0.

Functions can receive a variable number of arguments but two arguments are default: error and success messages.

Success messages can be suppressed if passed empty otherwise error messages will never be suppressed.

By standard the last two arguments of hc functions are respectively the error message and the success message:

    include ~/hc/hc_gcc_version.hsl
    (...)
    $gcc_is_ok = hc_gcc_version(">",
                                "1.0.0",
                                "You must update your gcc... tetanus can be dangerous!",
                                "GCC greater than 1.0.0 good dog!");
    (...)

All hc functions are under the "hc" include directory.

Following you'll find descriptions about the main hc functions and how to use them.

# More about some hc functions

This section and following subsections are organized by modules (e.g.: files under hc/ subdirectory). The
documentation here is rather straightforward: the subsection named as the related hc source file, some commentary
about and an example. So...

## "hc/hc.hsl"

This file doesn't have anything special (except two functions, ok, so there are things) to be used by hc function users,
because here is coded common functions which can be used by another hc modules.

### hc_set_abort_on_fail()

The default behavior when a hc check fails is continue the following checks, letting to user at the end of the checking
process to decide if it's better abort the build process or not.

If you want to abort you need to call hc_set_abort_on_fail() before start any hc check, something like this:

    include ~/hc/hc.hsl

    conquer-the-world.prologue() {

        hc_set_abort_on_fail();

        hc_check_my_killer_droids();

    }


### hc_unset_abort_on_fail()

It does the opposite of hc_set_abort_on_fail(), so when some hc check fails, the whole (main) process still continue.

    include ~/hc/hc.hsl

    conquer-the-world.prologue() {

        hc_set_abort_on_fail();

        hc_check_my_killer_droids();

        hc_unset_abort_on_fail();

        hc_check_my_bathroom(); # smelly but acceptable.

    }


### hc_should_abort_on_fail()

It returns 1 if the process should be aborted otherwise 0. With hc_should_abort_on_fail() returning 0, it means that you need
to control what specifically to do in this situation... try to fix the environment, to adapt your build... It depends on you.

    include ~/hc/hc.hsl
    include ~/not.hsl
    include hc_check_my_lasers_cannons.hsl

    conquer-the-world.prologue() {

        hc_check_my_killer_droids();

        hc_unset_abort_on_fail();

        hc_check_my_bathroom(); # smelly but acceptable.

        var ok type int;

        $ok =  hc_check_my_lasers_cannons(101, "Houston, guess what...", "MuHauahuhauHa!");

        if (not(hc_should_abort_on_fail())) {

            if (not($ok)) {

                $ok = call_my_moles_army();

            }

            if (not($ok)) {

                freakout("# %1_@&**!");

                hefesto.project.abort(1); # f_ck!

            }

        }

    }


### hc_print_result()

This function should be used by hc modules developers. It's used to print error or success messages and abort the process
when necessary (on errors of course).

    # meanwhile inside some hc module source code...

    # "hc_check_my_lasers_cannons.hsl"

    include ~/hc/hc.hsl

    function hc_check_my_lasers_cannons(zeta_coord type int, error_message type string,
                                        success_message type string) : result type int {

        hc_print_result("hc_check_my_lasers_cannons()", 0, $error_message, $success_message); # freak....

        result 0; # put here by some mature hc devel mole.

    }

    function call_my_moles_army() : result type int {

        result (1 == 0);

    }

    function freakout(ncallings type string) : result type none {

        hefesto.sys.run("cat \""  + $ncallings + "\" > /dev/null");

    }

    # Zzz...

## "hc/hc_gcc_export.hsl"

In this file you'll find the function hc_gcc_export(), which verifies if gcc can be called without any problems from the
current working directory in order to generate a very basic binary.

So the usage of it:

    include ~/hc/hc_gcc_export.hsl
    include ~/hc/hc.hsl

    c-gcc-only-project.prologue() {

        hc_set_abort_on_fail();

        hc_gcc_export("Please, check if your GCC's path is exported.", "GCC seems ok.");

    }

## "hc/hc_javac_export.hsl"

This file brings a function that can be used to check if Java compiler's path is exported on your environment.

You can use as follows:

    include ~/hc/hc.hsl
    include ~/hc/hc_javac_export.hsl

    j-another-j-example.prologue() {

        hc_set_abort_on_fail();

        hc_javac_export("Please, j-check if your javac's j-path is j-exported.", "Javac seems j-ok.");

    }


## "hc/hc_libgmp.hsl"

To verify if libgmp is installed on build environment you can use hc_libgmp() in this way:

    include ~/hc/hc.hsl
    include ~/hc/hc_libgmp.hsl

    my-zeta-function-seeker.prologue() {

        hc_set_abort_on_fail();

        hc_libgmp("No way man, libgmp is need here!", "Nice! libgmp is here! Let's make some history!");

    }


## "hc/hc_libpthread.hsl"

In order to verify if in current build enviroment we can link applications that uses Pthreads, we can use:

    include ~/hc/hc.hsl
    include ~/hc/hc_libpthread.hsl

    producer-consumer-lousy-sample-again-and-again.prologue() {

        hc_set_abort_on_fail();

        hc_libpthread("No way to build this innovative college sample without Pthreads library.",
                      "Ok, after you'll master all things about Multithreading.");

    }

## "hc/hc_python_export.hsl"

In order to verify the presence of python:

    include ~/hc/hc.hsl
    include ~/hc/hc_python_export.hsl

    python-sssssss-sssssss-niii-ahhh-dont-say-niiii-ahhhh.prologue() {

        hc_set_abort_on_fail();

        hc_python_export("I can't make coffee without python... We'll die!!! Please, pleeeease install it!",
                         "Python is here, I don't need to say THAT word....\n- Ni?...\nArrghhhhhh!!!");

    }

## "hc/boost_version.hsl"

Ok, you're use boost, so what version you're using... Hummm and you need to THAT version... all right?...

There's a way:

    include ~/hc/hc.hsl
    include ~/hc/hc_boost_version.hsl

    my-blase-cpp.prologue() {

        hc_set_abort_on_fail();

        hc_boost_version("=",
                         "1_42",
                         "I need boost 1.42 dumb human...",
                         "Ok, you got what I need... you're still alive...");

    }

The first argument is releated with the type of version checking... it can be: "=", ">", ">=", "<", "<="  or "!=".

The second is the version, formatted as defined in "boost_version.hpp" header file.

## "hc/gcc_version.hsl"

Sometimes is needed compile things using specific GCC version (oh God... why?!!)....

So for crazy situations, you could include this.....madness:

    include ~/hc/hc.hsl
    include ~/hc/hc_gcc_version.hsl

    my-mad-maganize-c-reader.prologue() {

        hc_set_abort_on_fail();

        hc_gcc_version(">=", "4.8.0", "GCC version must be >= 4.8.0", "GCC >= 4.8.0... It's good... gooooood!");

    }

## "hc/hc_jvm_export.hsl"

When you for some reason need to verify JVM installation, use this:

    include ~/hc/hc.hsl
    include ~/hc/hc_jvm_export.hsl

    function new_jvm_jcheck() : result type none {

        hc_jvm_export("JVM j-seems j-not j-installed.", "JVM j-is j-installed... j-good j-doooog! j-he j-he j-he!");

    }

    j-jvm-j-sample.prologue() {

        hc_set_abort_on_fail();

        new_jvm_jcheck();

    }

But not in this bureaucratic way, please! :)

## "hc/hc_libncurses.hsl"

If your application uses libcurses, use it to check if it can be well-linked on current build environment.

    include ~/hc/hc.hsl
    include ~/hc/hc_libncurses.hsl

    my-libcurses-proj.prologue() {

        hc_set_abort_on_fail();

        hc_libncurses("Man... I need Ncurses... It's serious... otherwise you could cry...", ""); # Nothing will be said on ok situations.

    }

## "hc/hc_linux_distro.hsl"

Sometimes depending on what Linux distro your build is running you need to do thing A otherwise thing B.

In this case, use this hc function:

    include ~/hc/hc_linux_distro.hsl

    my-lnx-project.prologue() {

        $sources.ls(".*\\.c$");

        var special_distros type list;

        $special_distros.add_item("slackware");

        $special_distros.add_item("red hat");

        $special_distros.add_item("centos");

        if (hc_linux_distro($special_distros,
                            1,
                            "We need to compile additional code too.",
                            "That all right nothing additional to compile.") == 0) {

            hefesto.sys.cd("stubs");

            hefesto.sys.ls(".*\\.c$");

            hefesto.sys.cd("..");

        }

    }

The first argument is a list containing all expected distros names.

The second indicates that the name comparison is no-case (1).


## "hc/hc_type_socklen_t"

This hc function is used to check if the type socklen_t is defined on the current system.

    include ~/hc/hc_type_socklen_t.hsl
    include ~/hc/hc.hsl

    s0ck3t-hx0rs-send-recv-awesome-revelations.prologue() { # tsc, tsc.....

        hc_set_abort_on_fail();

        hc_type_socklen_t("The socklen_t type isn't present, replace it for int.", "");

    }


## "hc/hc_cpu.hsl"

This module has two functions "hc_cpu32()" and "hc_cpu64()". Both verify the processor word-size (32 and 64 respectively).

    include ~/hc/hc_cpu.hsl

    processor-dependant-project.prologue() {

        if (hc_cpu32("Some codes will be adjusted, wait....", "No code to be adjusted.") == 0) {

            setup_code64();

        }

    }


## "hc/hc_libcrypt.hsl"

This verifies the presence of libcrypt on the current build environment.

    include ~/hc/hc_libcrypt.hsl
    include ~/hc/hc.hsl

    pass-cracker.prologue() {

        hc_set_abort_on_fail();

        hc_libcrypt("I need libcrypt!", "Libcrypt is here... good.");

    }


## "hc/hc_libpcap.hsl"

To check if the current build environment can link applications that use libpcap. Try it:

    include ~/hc/hc_libpcap.hsl
    include ~/hc/hc.hsl

    snowblind.prologue() {

        hc_set_abort_on_fail();

        hc_libpcap("Unable to find libpcap.", "");

    }


## "hc/hc_perl_export.hsl"

If you need Perl for some reason, use it to verify if Perl is accessible:

    include ~/hc/hc.hsl
    include ~/hc/hc_perl_export.hsl

    my-project.prologue() {

        hc_set_abort_on_fail();

        hc_perl_export("I couldn't find Perl.", "");

    }


## "hc/hc_user_account.hsl"

If your project need a specific user account... you can use it to check this account:

    include ~/hc/hc_user_account.hsl

    my-server.epilogue() {

        hc_user_account("my_server_user",
                        "WARNING: my_server_user seems not created, you can have problems with it, be aware...", "");

    }


## "hc/hc_execinfo.hsl"

If your project generates GCC's backtraces the execinfo library is necessary, then to verify if the current build
environment can handle codes with this:

    include ~/hc/hc.hsl
    include ~/hc/hc_execinfo.hsl

    my-segfault-random-generator.preloading() {

        hc_set_abort_on_fail();

        hc_execinfo("NO execinfo... the toolset won't be loaded... bye!",
                    "Nice... execinfo is here... now I'll load the toolset.");

    }
