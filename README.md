# Helios

## What is this?

Helios is an acronym for [He]festo [li]brary and [o]ther [s]tuffs.

This project is destinated to gather HSL codes which can be useful to integrate on [Hefesto](https://github.com/rafael-santiago/hefesto.git)
as extensions for the standard library besides the own standard library.

When you install [Hefesto](https://github.com/rafael-santiago/hefesto.git) a very basic library is copied to your system and
maybe if you really liked Hefesto's proposal maybe you want to expand your standard library to build and/or automate more things
than just compile C/C++ projects for example.

Here you can find more toolsets destinated for several programming languages besides common purpose functionalities.

And yes, it can be understood as an official Hefesto's extensions repository.

## Understanding the Helio's basic directory structure

    helios/                                     [The Helios' root directory.]
          doc/                                  [A place destinated to documentation.]
          installer/                            [All installer/uninstaller infrastructure is here]
          src/                                  [The Helios' src root directory]
               includes/                        [Here the common purpose HSL code can be or at least subdirectories containing it...]
                       toolsets/                [...but HSL codes which composes toolsets must be here.]
                                common/         [Sometimes toolsets can share a code base so here is a place for it.]
               modules/                         [Modules (E.g.: HSL codes which uses a native portion) must be placed here.]

## How to access the Helios catalog to know more about available extensions?

Being inside Helios' root directory just type: "hefesto --helios-catalog=<extension-name>".

## Understading the catalog files.

A catalog file is just a plain file named in form "<extension-name>-catalog" which must be placed in the same related extension's directory.

## Understanding the "src/hstd.base"

When you add to Helios new features (E.g.: new toolsets or new common purpose codes) you need to do some registration in order
to make your new stuff visible to helios install system. Basically you need to do two things:

The first one is add to "src/hstd.base" a new line in this form:

# Extension name        # Extension's root directory
extension-name          extension-root-directory/

The second one is create a file under "src" subdirectory named "extension-name.files" and inside of it you need list each file that composes
your new extension (being one file per line using relative file paths only).

Now in order to test your new extension visibility... inside the Helios' root directory type: "hefesto --new-stuff-sanity-check=<extension-name>".

Or still: "hefesto --hstd-check"

## How to install new things to my working standard library

Being inside Helios' root directory just type: "hefesto --install-<extension-name-listed-on-helios-catalog>".

## How to uninstall things from my working standard library

Being inside Helios' root directory just type: "hefesto --uninstall-<extension-name-listed-on-helios-catalog>".

Warning: this operation doesn't take in consideration any dependency among other installed extensions in your system.

## How to contribute

Just open a pull request and welcome and thank you in advance! :)

Enjoy!

Santiago
