## Building

1. Install [Visual Studio IDE](https://visualstudio.microsoft.com/). Visual Studio is needed to perform a build.
2. Use Visual Studio Installer to install the following development tools:
* Windows 11 Software Development Kit, version 22621. You do not have to install Windows 11, this SDK can be used on Windows 10.
* Windows Universal CRT SDK
* C++ build tools MSVC v140 for Visual Studio 2015
* C++ x64/x86 build tools MSVC v143 for Visual Studio 2022
* C++ ARM build tools MSVC v143 for Visual Studio 2022
* C++ ARM64/ARM64EC build tools MSVC v143 for Visual Studio 2022
* English language pack

The need to install C++ ARM build tools seems to look confusing because the build is targeted at the complex instruction set computer architecture. These requirements are introduced by [this change](https://github.com/python/cpython/commit/45faf151c693b6f13f78926761caea6df7242024), after which Windows Installer XML Toolset requires ARM build tools even if a solution is not targeted at ARM devices. [More information about this can be found here](https://github.com/python/cpython/issues/106765).

3. Install one of the following on the host machine:
* [Specific build of CPython interpreter 3.9](https://github.com/vladimir-andreevich/cpython-windows-vista-and-7/blob/main/v3.9/python-3.9.13-amd64-full.exe)
* [Specific build of CPython interpreter 3.10](https://github.com/vladimir-andreevich/cpython-windows-vista-and-7/blob/main/v3.10/python-3.10.11-amd64-full.exe)
4. Install Sphinx 7.2.6 to this Python interpreter: ```pip install Sphinx==7.2.6```. You are free to install Sphinx in a virtual Python environment.
5. Download the source code from this repository as ZIP. I do not recommend using Git. In case some issue happens, this repository may be force pushed. Unpack to a path that does not contain spaces. Otherwise, you may get an error 9009 when executing ```gendef```.
6. Go to Settings -> System -> About -> Advanced system settings -> Environment variables. You can work in the section with system variables as well as in the section with user variables.
* Add a new variable ```PATCHDIR``` and set its value to ```where_you_have_unpacked_zip\cpython-windows-vista-and-7\v3.11\Python-3.11.9\api-ms-win-core-path-HACK```. This folder should contain ```x86\api-ms-win-core-path-l1-1-0.dll``` and ```x64\api-ms-win-core-path-l1-1-0.dll```.
* Add a new variable ```PYTHON``` and set its value to the location of the interpreter where Sphinx 7.2.6 is installed. For example, ```PYTHON = C:\Users\User\AppData\Local\Programs\Python\Python310\python.exe```. In order to check where your Python interpreter is located, type ```where python``` in the command line.
7. In the terminal, go to the folder with the Python 3.11 source code and run ```.\Tools\msi\buildrelease.bat -x86 -x64```. If you get an error during the documentation build saying that ```itircl.dll``` was not registered correctly, go to ```externals\windows-installer\htmlhelp``` and run ```regsvr32 itcc.dll```. Another solution to this problem is installing HTML Help Compiler system-wide, which registers this DLL anyway.
8. Obtain installers and embeddable packages from ```.\PCbuild\amd64\en-us``` and ```.\PCbuild\win32\en-us``` and enjoy problem solving with Python!
