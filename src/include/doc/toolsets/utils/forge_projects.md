# The forge_projects.hsl module

This module brings a ``HSL`` function which can recurssivelly run forges from specified subdirectories that have a pre-configurated invocation file.

## Default location of this module

>``include ~/toolsets/utils/forge_projects.hsl``

## The ``forge_projects()`` function

This function is the bootstrapper which receives a list containing all relevant subdirectories which possible have the ``.ivk`` file. If some error occurs during the process this function results something different of *0*.

>``$exit_code = forge_projects($subdirectories_with_subprojects);``
