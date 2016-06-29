# Tulip-v3's toolset

This ``HSL`` code collection brings some functions in order to automate the tablatures generation using
[``Tulip``](https://github.com/rafael-santiago/tulip).

## Writing a basic tulip-v3's forgefile

Supposing that you have installed the discussed toolset using the [``helios'``](https://github.com/rafael-santiago/helios)
install system. You need to include the following ``HSL`` from inside your ``HSL`` script:

```
include ~/toolset/tulip/tulip-v3.hsl
```

The ``tulip-v3 toolset's`` forge function receives one ``list`` as argument. This list should contain the
``.tlp`` files to be processed. If you pass a empty list, the toolset will try to find all ``tlp's`` in the
current directory.

Follows a basic [``hefesto's``](https://github.com/rafael-santiago/hefesto) project for [``tulip-v3``](https://github.com/rafael-santiago/tulip)
example:

```
include ~/toolset/tulip/tulip-v3.hsl

var sources type list;

project tulip-v3-sample : toolset "tulip-v3" : $sources;

tulip-v3-sample.prologue() {
    $sources.ls(".*\\.tlp$");
}
```

Done, here we get a inconditional forge. What means that every time all found ``.tlp`` files will be reprocessed
even without any change.

## Adding a dependency chain to your forge

The ``tulip-v3 toolset's`` uses the same old dependency scanner used by ``tulip-v2`` and ``tulip-v1``. Follows sample
that composes a dependency chain:

```
include ~/toolset/tulip/tulip-v3.hsl
include ~/toolset/tulip/get_tlp_deps.hsl

var sources type list;
var deps type string;

project tulip-v3-sample : toolset "tulip-v3" : dependencies $deps : $sources;

tulip-v3-sample.prologue() {
    $sources.ls("*.\\.tlp$");
    $deps = get_tlp_deps($sources);
}
```

Done, here we get a conditional forge. What means that on each invoked forge only changed files will be reprocessed.

## Tulip-v3 toolset's internal options

Take a look at the **Table 1** to know more about the available options.

**Table 1**: Internal toolset's option.

|         **Toolset option**               |                **Handy for**                                         |
|:----------------------------------------:|:--------------------------------------------------------------------:|
|             ``--just-compile``           |           Just compile the ``tlp`` scripts                           |
|            ``--out-type=<type>``         | Specifying the tablature output type (``txt``, ``ps``, ``pdf``)      |
|       ``--tab-output-dir=<dirpath>``     | Specifying a directory where all generated tablatures will be placed |

These options should be passed during the [``hefesto's``](https://github.com/rafael-santiago/hefesto) invocation.

Remark: the ``--tab-output-dir`` will create the ``sub-directory`` if needed. However, it can not create a brand new directory tree.
