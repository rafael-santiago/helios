# The null toolset

This toolset is merely a *stub* that you can use to test some ``HSL`` code that you wrote.

The basic usage of it includes:

1. Define a project that uses this null toolset.
2. Use some of project ``entry-points`` in order to test your code.

Follows an example:

        # ``test.hsl``
        include ~/toolsets/null/null.hsl

        project hsl-tester : toolset "no-tool-any-set" : 0;

        function function_to_be_tested() : result type none {
            hefesto.sys.echo("Some stuff goes here.\n");
        }

        hsl-tester.prologue() {
            function_to_be_tested();
        }

Running your test:

>``hefesto --forgefiles=test.hsl --test-projects=hsl-tester``

