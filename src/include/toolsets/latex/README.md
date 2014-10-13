# The Hefesto's LaTeX toolset

The Hefesto's LaTeX toolset assist you on basic .dvi generation
and also genarates the pdf too.

To start to use it you need to include the toolset definition:

    include ~/toolsets/latex/latex.hsl

After, you must to declare your project, telling that it uses the
LaTeX, look:

    project my_next_pulitzer : toolset "LaTeX" : "mybook.tex" ;

You only need to pass the name of your main .tex file to forge function.

To compile your tex:

    hefesto --forgefiles=example.hsl --example-projects=my_next_pulitzer

If you need to pass some option to latex, use:

    hefesto --forgefiles=example.hsl --example-projects=my_next_pulitzer --latex-options=youropt

It's very simple, you could create a template to be used in any latex project, look:

    include ~/toolsets/latex/latex.hsl

    var main_tex_filename type string;

    project carbonEx : toolset "LaTeX" : $main_tex_filename ;

    cabonEx.prologue()
    {
        var maintex type list;
        $maintex = hefesto.sys.get_option("main-tex");
        if ($maintex.count() == 0) {
            hefesto.sys.echo("ERROR: you must to indicate the main .tex file with --main-tex option.\n");
            hefesto.sys.exit(1);
        }
        $main_text_filename = $maintex.item(0);
        hefesto.sys.echo("*** You are using CarbonEx template v0.1 ***\n");
    }

    carbonEx.epilogue()
    {
        hefesto.sys.echo("***\n");
    }

Now, to compile with this template:

    hefesto --forgefiles=cabonEx.hsl --carbonEx-projects=carbonEx --main-tex=mybook.tex

But it's only a sugestion...

In order to generate the pdf from .dvi you must pass the command option --mkpdf:

    hefesto --forgefiles=example.hsl --example-projects=my_next_pulitzer --mkpdf

Ok, you want to specify the pdf file name:

    hefesto --forgefiles=example.hsl --example-projects=my_next_pulitzer --mkpdf --pdfout=T-hooooooowl.pdf

The latex creates some files that you maybe want to delete them... which keeps your directory always clean:

    hefesto --forgefiles=example.hsl --example-projects=my_next_pulitzer --keepclean

The command option "--keepclean" will removes all ".log" and ".aux" from the current directory.

Thats it... Enjoy!
