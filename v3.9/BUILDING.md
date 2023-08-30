## Building

1. Install Visual Studio IDE 2019. Visual Studio is needed to perform a build.
2. Use Visual Studio Installer to install the following development tools:
* Windows 11 Software Development Kit, version 22000. You do not have to install Windows 11, this SDK can be used on Windows 10.
* Windows Universal CRT SDK
* C++ build tools MSVC v140 for Visual Studio 2015
* C++ x64/x86 build tools MSVC v142 for Visual Studio 2019
* .NET Framework 3.5 development tools
* English language pack
3. Install the [CPython interpreter](https://www.python.org/), version 3.6 or 3.7 or 3.8 on the host machine.
4. Install Sphinx 3.5.4 to this Python interpreter: ```pip install Sphinx==3.5.4```. You are free to install Sphinx in a virtual Python environment.
5. Make sure that Sphinx 3.5.4, installed in the previous step, uses version 3.0.3 of Jinja2 template engine: ```pip install Jinja2==3.0.3```. In case you do not check it, the compilation might fail later with the error ```LGHT0103``` saying that the system cannot find the CHM documentation file. [More information about this issue can be found here](https://github.com/python/cpython/issues/92738).
6. Download the source code from this repository as ZIP. I do not recommend using Git. In case some issue happens, this repository may be force pushed. Unpack to a path that does not contain spaces. Otherwise, you may get an error 9009 when executing ```gendef```.
7. Go to Settings -> System -> About -> Advanced system settings -> Environment variables. You can work in the section with system variables as well as in the section with user variables.
* Add a new variable ```PATCHDIR``` and set its value to ```where_you_have_unpacked_zip\cpython-windows-vista-and-7\v3.9\Python-3.9.13\api-ms-win-core-path-HACK```. This folder should contain ```x86\api-ms-win-core-path-l1-1-0.dll``` and ```x64\api-ms-win-core-path-l1-1-0.dll```.
* Add a new variable ```PYTHON``` and set its value to the location of the interpreter where Sphinx 3.5.4 is installed. For example, ```PYTHON = C:\Users\User\AppData\Local\Programs\Python\Python38\python.exe```. In order to check where your Python interpreter is located, type ```where python``` in the command line.
8. In the terminal, go to the folder with the Python 3.9 source code and run ```.\Tools\msi\buildrelease.bat -x86 -x64```. If you get an error during the documentation build saying that ```itircl.dll``` was not registered correctly, go to ```externals\windows-installer\htmlhelp``` and run ```regsvr32 itcc.dll```. Another solution to this problem is installing HTML Help Compiler system-wide, which registers this DLL anyway.
9. Obtain installers and embeddable packages from ```.\PCbuild\amd64\en-us``` and ```.\PCbuild\win32\en-us``` and enjoy problem solving with Python!
