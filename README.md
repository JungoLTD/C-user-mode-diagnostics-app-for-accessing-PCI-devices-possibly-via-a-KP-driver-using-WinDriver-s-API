# C-user-mode-diagnostics-app-for-accessing-PCI-devices-possibly-via-a-KP-driver-using-WinDriver-s-API
This directory contains C# code of a diagnostics WinDriver PCI library, as well as user-mode console application (pci_diag). which use the sample library API. 


**WinDriver PCI diagnostic console C# sample**
The source code for this project is provided with Jungo WinDriver. To compile this application, you will need a compiler and CMake installed.
**Overview**
An INF must be installed in order for Windows to access and control the PCI device. You can generate and install INF files via the DriverWizard,
or install an existing INF file with 'wdreg.exe'. This sample allows scanning the PCI bus to locate a specific device and retrieve its resource
information, reading/writing from/to a specific address or register, reading/writing from/to the PCI configuration space, handling interrupts from the
PCI device and registering Plug and Play and power management events for the device.
**Files**
pci_diag.cs - The main file, which demonstrates controlling a PCI device using the shared library files.
**../shared/diag_lib.cs, ../shared/pci_lib.cs, ../shared/wdc_diag_lib.cs, ../shared/wds_diag_lib.cs** - The library files, which use WinDriver High-Level APIs to access and control PCI devices. These APIs are defined in wdapi1610.dll andare wrapped for .NET Core in wdapi_netcore1610.dll.
**CMakeLists.txt** - An input file for the CMake build system.
**readme.pdf** - Describes the sample files.

We provide several methods for compiling this code:

**Compiling this project using Microsoft Visual Studio/Visual Studio Code**
- If you are using Microsoft Visual Studio 2017 or higher, or Visual Studio Code, make sure to have CMake support installed for it.
- When you open the sample folder (with File->Open->Folder...) or open the CMakeLists.txt file (with File->Open->CMake...), VisualStudio will automatically invoke the cmake command to generate a CMake cache for the project. To generate cache manually, press the 'Switch between solutions and available views' button, right click on the CMake project and select 'Generate Cache'.
 - Expand the CMake project - all available targets for the project will be listed.
 - Right clicking on the target will allow you to build it.
 - 
**Compiling using a different IDE/Compiler:**
Run the following command in the terminal from the working directory of the project:
$ cmake . -B build
This will create a Unix Makefile for the project in a new sub-directory named build. To build it, go to that sub-directory and run:
$ make
To add verbosity to a build you can run:
$ VERBOSE=1 make
or if you prefer the build to always be verbose you can generate the CMake cache in the following way:
$ cmake . -B build -DCMAKE_VERBOSE_MAKEFILE=ON
You can use CMake to generate projects for various other platforms and IDEs. Consult CMake's documentation for more information.

**Compiling this project using dotnet:**
Build
Run the following command from the directory containing the .csproj file:
$ dotnet build [project file] -p:Configuration=Release
This command builds the project and its dependencies and creates an executable that can be used to run the application (the hosting system must
have the .NET shared runtime installed on it in order to run the executable).
Publish
Run the following command from the directory containing the .csproj file:
$ dotnet publish [project file] --use-current-runtime
$ dotnet publish [project file] --r <runtime id>
This command builds the project and its dependencies and creates a platform-specific executable ready for deployment on a host system. Please
note that it is not necessary for for the .NET shared runtime to be installed on the host system for the executable to work.

**Converting to a GUI application:**
This sample was written as a console mode application (rather than a GUI application) that uses standard input and output. This was done in order
to simplify the source code. You may change it into a GUI application by removing all calls to printf() and scanf() functions, and calling
MessageBox() instead (on Windows). On other operating systems, you can use the relevant libraries such as GTK or Qt.
