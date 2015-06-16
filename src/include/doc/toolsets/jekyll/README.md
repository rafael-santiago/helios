# The Jekyll Toolset

This toolset is a pretty simple piece of ``HSL`` to use. Basically it allows you ``build``, ``preview`` or ``publish`` a site
using ``Jekyll``.

The Forgefile for it could be something like:

        # "_Forgefile.hsl"
        include ~/toolsets/jekyll/jekyll.hsl

        project your-site : toolset "jekyll" : ;

In order to make the things simple you should use an invocation file:

        --forgefiles=_Forgefile.hsl --_Forgefile-projects=your-site

All operations must be called from the root of your project directory.

So if you want to build:

``hefesto --build``

If you want to preview:

``hefesto --preview``

If you want to publish (it uses ``Git``):

``hefesto --publish``

If you want to do all together:

``hefesto --build --preview --publish``

Note that the preview mode offers choices to continue the process, rebuild the site or abort the process.
