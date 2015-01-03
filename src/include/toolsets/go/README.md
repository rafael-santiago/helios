# The Go toolset

With this toolset you can automate the "go build" command don't worrying about if there are several go programs in the
current working directory.

For example, supposing that we have this directory status:

    root@zephyr:~/src/1-2-3-go# ls -1
    for.go
    func.go
    func_multi.go
    hello.go
    if-else.go
    map.go
    range.go
    slices.go
    switch.go
    variables.go
    variadic.go

Each file which resides in this directory has the following Go declaration:

    package main

So, if you try:

    root@zephyr:~/src/1-2-3-go# go build

You'll get an error based on something like "main redeclared... blah-blah..."...

With this Go toolset you can generate each binary without any problem, look:

    # Forgefile.hsl

    include ~/toolset/go/go.hsl

    var gofiles type list;

    project go-samples : toolset "go" : $gofiles;

    go-samples.prologue() {
        $gofiles = hefesto.sys.get_option("gofiles");
    }

Ok, then we try:

    root@zephyr:~/src/1-2-3-go# hefesto --forgefiles=Forgefile.hsl --Forgefile-projects=go-sample
    root@zephyr:~/src/1-2-3-go# ls -1
    for*
    for.go
    func*
    func.go
    func_multi*
    func_multi.go
    hello*
    hello.go
    if-else*
    if-else.go
    map*
    map.go
    range*
    range.go
    slices*
    slices.go
    switch*
    switch.go
    variables*
    variables.go
    variadic*
    variadic.go

Now we got our binaries... but there is an inconvenience here... if you try to invoke the project forge again...
all will build again but without any necessity.

Fortunately, this go toolset supports the dep-chain too. Let's edit the "Forgefile.hsl" from last sample:

    # Forgefile.hsl

    include ~/toolset/go/go.hsl
    include ~/toolset/go/common/get_gofiles_deps.hsl # the dep-chain scanner is defined here...

    var gofiles type list;
    var deps type string;

    project go-samples : toolset "go" : dependencies $deps : $gofiles; # Now any file change will be watched

    go-samples.prologue() {
        $deps = get_gofiles_deps(); # get the relevant dependencies among files in the current working directory.
        $gofiles = hefesto.sys.get_option("gofiles");
    }

Now, if you call hefesto again... all go files will be built... but if you call it over again, none of them will be built...
because no changes were detected since the last assisted forge.

Based on our state of things, another useful thing to create is an ".ivk" file with this content:

    --forgefiles=Forgefile.hsl --Forgefile-projects=go-sample

After this, we can call go-sample's forge in an easier way:

    root@zephyr:~/src/1-2-3-go# hefesto

## Toolset options

This toolset has only to user-options:

    * gofiles=gofile_a.go,gofile_b.go,(...),gofile_y.go,gofile_z.go
    * goclean

The option "gofiles" is used to specify which files in the current directory will be built. If this option is not supplied
the toolset internally includes all go files from current directory, so that alien line in the "Forgefile.hsl" is now
understood:

    # Forgefile.hsl

    include ~/toolset/go/go.hsl
    include ~/toolset/go/common/get_gofiles_deps.hsl

    var gofiles type list;
    var deps type string;

    project go-samples : toolset "go" : dependencies $deps : $gofiles;

    go-samples.prologue() {
        $deps = get_gofiles_deps();
        $gofiles = hefesto.sys.get_option("gofiles"); # Oh! My God, Rafael is a crazy guy... tsc, tsc....
    }

Follows a gofiles option usage:

    Napoleon@zephyr:~/src/1-2-3-go# hefesto --gofiles=for.go,func.go,map.go,variadic.go


The option "goclean" is used if you want to delete all generate binaries in the current directory. If there is a pratical
".ivk" file inside our example directory... to clean up it:

    root@zephyr:~/src/1-2-3-go# hefesto --goclean
    (...)
    root@zephyr:~/src/1-2-3-go# ls -1
    for.go
    func.go
    func_multi.go
    hello.go
    if-else.go
    map.go
    range.go
    slices.go
    switch.go
    variables.go
    variadic.go

Easy...

You need to know that the "goclean" option has precedence over the "gofiles" option.

Now you master all about this simple Go toolset :)

Enjoy!

