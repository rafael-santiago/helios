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

