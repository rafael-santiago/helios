# The Hefesto's Linux module toolset

You should use this toolset in order to abstract the ``KBuild`` usage.

To start to use it you need to include the toolset definition:

```
include ~/toolsets/linux/linux-module.hsl
```

After you need to declare your linux module project saying that it
uses the ``linux-module`` toolset.

```
var includes type list;
var cflags type list;
var libraries type list;
var ldflags type list;

project scull-dev : toolset "linux-lkm" : "main-module-source.c", $includes, $cflags,
                                                                  $libraries, $ldflags,
                                                                  "scull";
```

The arguments received by its forge function are:

- The source code which stands for your main module's source.
- A list containing the additional includes directories.
- A list containing the additional compiler flags.
- A list containing the additional libraries directories.
- A list containing the additional linker flags.
- The name of your kernel object file.

Once all defined, supposing that you have saved it into ``Forgefile.hsl``, you should invoke ``Hefesto`` as follows:

```
hefesto --forgefile=Forgefile.hsl --Forgefile-projects=scull-dev
```

If you want to abstract a little more you should create an ``.ivk`` file and put the following forge parameters into it:

```
--forgefile=Forgefile.hsl --Forgefile-projects=scull-dev
```

Now the forge invocation became easier:

```
hefesto
```

## Important remarks

The ``KBuild`` runs from the kernel source tree. Then if you intend to use additional includes/libraries directories it
is pretty important specify full paths for them. Look:

```
scull-dev.prologue() {
    $includes.add_item(hefesto.sys.make_path(hefesto.sys.pwd(), "foo"));
    $libraries.add_item(hefesto.sys.make_path(hefesto.sys.pwd(), "bar"));
    $ldflags.add_item("-lbar");
}
```

You should not mind about ``*.mod.c`` files. They are automatically generated.


Well, now I think that you master everything here. Congrats!

Enjoy!
