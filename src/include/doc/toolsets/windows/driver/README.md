# The Hefesto's toolset for Windows' drivers

This toolset makes possible Windows drivers building through Hefesto.

All you should do is include the main toolset file:

	include ~/toolsets/windows/driver/windows-driver.hsl
	
After you need to declare the project by using the toolset ``windows-driver``. The project takes a
source list, includes list, compiler flags list, libraries list, linker flags list and the target name:

	local var src type list;
	local var includes type list;
	local var cflags type list;
	local var libraries type list;
	local var ldflags type list;

	project test-driver : toolset "windows-driver" : 
					$src, $includes, $cflags, $libraries, $ldflags, "test-driver.sys";

When you pass a empty source list the toolset will try to scan the current working directory
for .c files.

When you need to define some symbol, you need to define it into compiler flags list in the following
form:

	$cflags.add_item("-DSymbol=something");
	
You can switch configuration and platform by using ``--compile-model`` and ``--cpu-arch`` toolset options.

The option ``--compile-model`` accepts ``release`` or ``debug`` (default).

The option ``--cpu-arch`` accepts a platform recognized by ``Msbuild``. ``x86`` is translated to ``Win32``.
When not specified the architecture is driven by the current build machine processor architecture.

You can you ``--inf`` to specify a .inf file. When not specified will be infered a inf named with the same
name of the target saved into the directory where build was called, e.g: ``target.sys``, expected ``target.inf``.
When an inf file is not specified through ``--inf`` option and an inferred is not found, a default one is automatically
generated. You can change it according your preferences and use it as a regular project file.

When a vcxproj having the same name of the target (e.g.: target.sys -> target.vcxproj) is found in the same
directory where build was called, this vcxproj will be used. When no vcxproj is found, one is generated and
removed at the end of build task.

Some invocation samples (assuming a well-confgured ``.ivk``):

	* Release 32-bit driver: 

		hefesto --compile-model=release --cpu-arch=x86
		
		hefesto --compile-model=release --cpu-arch=Win32
	
	* Debug 32-bit driver:
	
		hefesto --compile-model=debug --cpu-arch=x86
		
		hefesto --compile-model=debug --cpu-arch=Win32
		
	* Release 64-bit driver:
	
		hefesto --compile-model=release --cpu-arch=x64
		
	* Debug 64-bit driver:
	
		hefesto --compile-model=debug --cpu-arch=x64

	* Debug taking into consideration build machine architecture:
	
		hefesto
		
	* Debug taking into consideration build machine and specifying inf file:
	
		hefesto --inf=foobar.inf
