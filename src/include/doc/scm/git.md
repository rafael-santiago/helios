# The git.hsl module

This is a collection of wrappers for common [``git``](http://git-scm.org) commands. The wrappers which do not receive any argument must be executed under the ``git`` repository path.

## Default location of this module

>``include ~/scm/git.hsl``

## The ``git_pull()`` function

This is a wrapper for the git pull command. This function results the result code of the external executed command.

>``$exit_code = git_pull(); # it is necessary change to the repo directory before...``

## The ``git_clone()`` function

This is a wrapper for the git clone command. It receives as arguments an url string and a local directory path string. This function results the result code of the external executed command.

>``$exit_code = git_clone("https://github.com/someone/some.git", "local_temp_dir");``

## The ``git_push()`` function

This is a wrapper for the git push command. It does not receive any argument and results the exit code of the external executed command.

>``$exit_code = git_push(); # it is necessary change to the repo directory before...``

## The ``git_add()`` function

This is a wrapper for the git add command. This wrapper function receives as argument the file path of the wanted file to be added to the git file tracking system. This function results the exit code of the external command.

>``$exit_code = git_add("subdir/new.file");``

## The ``git_checkout()`` function

This is a wrapper for the git checkout command. This function receives a file path which must be checked out and results the exit code of the external executed command.

>``$exit_code = git_checkout("subdir/dirty.file");``

## The ``git_rm()`` function

This is a wrapper for the git rm command. This function receives a file path which must be removed from the git base. This wrapper results the exit code of the external executed command.

>``$exit_code = git_rm("subdir/file.witch");``

## The ``git_branch()`` function

This is a wrapper for the git branch command. This function receives a branch name of the desired branch to be created. This wrapper results the exit code of the external executed command.

>``$exit_code = git_branch("experiment-1");``

## The ``git_tag()`` function

This is a wrapper for the git tag command. This function receives as arguments the new tag name and the commit id from the tag must be created. This function results the exit code of the external executed command.

>``$exit_code = git_tag("hellease", "deadbeeff");``

## The ``git_commit()`` function

This is a wrapper for the git commit command. This function receives as argument the commit message and results the exit code of the external executed command.

>``$exit_code = git_commit("publishing blah blah blah.");``
