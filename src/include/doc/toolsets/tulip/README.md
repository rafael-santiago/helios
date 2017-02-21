# Tulip-v4's toolset

This ``HSL`` code collection brings some functions in order to automate the building of tablatures using
[``Tulip``](https://github.com/rafael-santiago/tulip).

## Writing a basic tulip-v4's forgefile

Supposing that you have installed the discussed toolset using the [``helios'``](https://github.com/rafael-santiago/helios)
install system. You need to include the following ``HSL`` inside your ``HSL`` script:

```
include ~/toolset/tulip/tulip-v4.hsl
```

The ``tulip-v4 toolset's`` forge function receives one ``list`` as argument. This list should contain the
``.tlp`` files to be processed. If you pass a empty list, the toolset will try to find all ``tlp's`` in the
current directory.

Follows a basic [``hefesto's``](https://github.com/rafael-santiago/hefesto) project for [``tulip-v4``](https://github.com/rafael-santiago/tulip)
example:

```
include ~/toolset/tulip/tulip-v4.hsl

var sources type list;

project tulip-v4-sample : toolset "tulip-v4" : $sources;

tulip-v4-sample.prologue() {
    $sources.ls(".*\\.tlp$");
}
```

Done. We get a unconditional forge. What means that every time all found ``.tlp`` files will be reprocessed
even without any change.

## Adding a dependency chain to your forge

The ``tulip-v4 toolset's`` uses the same old dependency scanner used by ``tulip-v2`` and ``tulip-v1``. Follows a sample
that composes a dependency chain:

```
include ~/toolset/tulip/tulip-v4.hsl
include ~/toolset/tulip/get_tlp_deps.hsl

var sources type list;
var deps type string;

project tulip-v4-sample : toolset "tulip-v4" : dependencies $deps : $sources;

tulip-v4-sample.prologue() {
    $sources.ls("*.\\.tlp$");
    $deps = get_tlp_deps($sources);
}
```

Done. We get a conditional forge. What means that on each invoked forge only changed files will be reprocessed.

## Tulip-v4 toolset's internal options

Take a look at the **Table 1** to know more about the available options.

**Table 1**: Internal toolset's option.

|         **Toolset option**               |                **Useful for**                                                                |
|:----------------------------------------:|:--------------------------------------------------------------------------------------------:|
|             ``--just-compile``           |           Just compile the ``tlp`` scripts                                                   |
|            ``--out-type=<type>``         | Specifying the tablature output type (``txt``, ``ps``, ``pdf``, ``eps``, ``md`` and ``html``)|
|       ``--tab-output-dir=<dirpath>``     | Specifying a directory where all generated tablatures will be placed                         |

These options should be passed during the [``hefesto's``](https://github.com/rafael-santiago/hefesto) invocation.

Remark: the ``--tab-output-dir`` will create the ``sub-directory`` if needed. However, it cannot create a brand new directory tree.
