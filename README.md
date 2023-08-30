<img src="./python.png" alt="Python for Windows Vista and Windows 7"/>

# Python 3.9+ for Windows Vista and Windows 7

This repository contains installers of Python 3.9 and newer versions for Windows Vista and Windows 7 and the source code of the Python programming language which is adapted for Windows Vista and Windows 7 with the instructions on how to build it.

## Introduction

Python is a popular programming language that is widely used in almost all fields of software development. Python has been continuously evolving since its inception. However, one significant change that recently occurred in Python was the drop of support for Windows Vista and Windows 7. This decision has sparked a lot of debate among developers and users, with some supporting this change and others giving negative criticism about it.

## Theoretical background

Since version 3.9, Python requires ```api-ms-win-core-path-l1-1-0.dll``` which is absent in Windows Vista and Windows 7. Prior to version 3.9, the library was dynamically imported; starting from Python 3.9, [the dynamic load is replaced with a static import](https://github.com/izbyshev/cpython/commit/6a65eba44bfd82ccc8bed4b5c6dd6637549955d5) of ```api-ms-win-core-path-l1-1-0.dll``` which breaks the compatibility with Windows Vista and Windows 7.

Since the static import of ```api-ms-win-core-path-l1-1-0.dll``` is the only issue that prevents Python 3.9 and its newer versions from running on Windows Vista and Windows 7, let's build the interpreter in the following way: instead of asking for the file from Windows Vista and Windows 7, we can directly provide the file ```api-ms-win-core-path-l1-1-0.dll``` to the programming language while building it.

I give credit to [Aohan Dang](https://www.linkedin.com/in/aohan-dang-536643a7/), a professional software developer and Python enthusiast, who has provided a way to build Python with ```api-ms-win-core-path-l1-1-0.dll``` for Windows 7 which is used here. I go further and backport Python to Windows Vista. If you need installers just for Windows 7, you can visit [Aohan's repository](https://github.com/adang1345/PythonWin7).

## Building

Building instructions for different versions of the Python programming language are different. Each folder with each Python version has its building instructions.

## Where compatibility problems may arise

**The core interpreters and the standard libraries of the Python programming language run correctly on Windows Vista and Windows 7.** Nothing is cut or modified in the Python programming language itself, and the interpreters in these installers read the code in the same exact way as the interpreters in the official Python installers. However, in the future, you may experience compatibility issues with ```pip``` packages. The reason is that developers of these packages may drop support for Windows Vista and Windows 7 considering that officially Python 3.9 and newer versions are not intended for these operating systems. I cannot provide any help with such kind of trouble because I have no control over thousands of Python software packages. In this case, I recommend contacting the developer of the specific package which causes the compatibility issue.

## When do you publish Python 3.11?

I will start backporting Python 3.11 to Windows Vista and Windows 7 right after the final bugfix is released. According to [PEP 664](https://peps.python.org/pep-0664/), the final bugfix release is 3.11.9 which is expected to be released on Monday, 2024-04-01.

### See also: [Node.js 14+ for Windows 7](https://github.com/vladimir-andreevich/node.js-windows-7)
