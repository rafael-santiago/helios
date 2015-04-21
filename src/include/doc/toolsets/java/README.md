# The Hefesto's Java toolset


With this toolset you can compile Java source and also generate the ".jar".

The first thing to do is include the main toolset file inside your Forgefile
or JForgefile ;)

        include ~/toolsets/java/java.hsl
    
After you must indicate that your project compiles by java toolset.

        var mainSourceFile type string;
        var javacExtraOptions type list;
    
        project Jfoo : toolset "java" : $mainSourceFile, $javacExtraOptions ;
    
The forge function receives the main source file as a string and the extra compiler options
which must be a list.

You can use this example as a template, reading the main source file from command line and
the options too, look:

        Jfoo.prologue() {
            var mainSourceFileOpt type list;
            $mainSourceFileOpt = hefesto.sys.get_option("main-source-file");
            if ($mainSourceFileOpt.count() == 0) {
                hefesto.sys.echo("ERROR: you must to indicate the main source file by --main-source-file option");
                hefesto.sys.exit(1);
            }
            $mainSourceFile = $mainSourceFileOpt.item(0);
            $javacExtraOptions = hefesto.sys.get_option("javac-extra-options");
        }

To compile from the "hsl template" you must to pass something like this:

        hefesto --forgefiles=jfoo.hsl --jfoo-projects=Jfoo --main-source-file=Foo.java

If you prefer don't read the main source file from some command option, you must to
hardcode it, and the compilation line will be:

        hefesto --forgefiles=jfoo.hsl --jfoo-projects=Jfoo
    
In order to generate the jar file you only must to pass some options to hefesto, look:

        hefesto --forgefiles=jfoo.hsl --jfoo-projects=Jfoo --mk-jar --mk-jar-manifest
    
The command above generates the jar generating automatically the manifest file, if you want to
specify a manifest file:

        hefesto --forgefiles=jfoo.hsl --jfoo-projects=Jfoo --mk-jar --jar-manifest=mymanifest.txt
    
By default the jar file is named based on main source file (.java extension replaced to .jar), if
you want to use another name:

        hefesto --forgefiles=jfoo.hsl --jfoo-projects=Jfoo --mk-jar-manifest --mk-jar --jar-name="Jjar.jar"
