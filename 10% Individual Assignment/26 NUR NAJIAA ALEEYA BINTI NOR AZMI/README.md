# How to Install GCC Compiler using pkg Package Manager on FreeBSD

## Introduction
GCC stands for GNU Compiler Collection. It is a free software compiler system capable of compiling several programming languages, 
including C, C++, Objective-C, and Fortran. GCC is widely used in creating software for Unix-like systems and it has been adapted for various platforms, 
demonstrating its adaptability and flexibility in the realm of open-source programming.

## Install GCC Compiler from FreeBSD Repository
There are 4 steps to install GCC, but make sure you have already downloaded `FreeBSD` on your PC before you start.

### Step 1: Open terminal on FreeBSD
The terminal takes the input from the user in the form of commands and displays the output on the screen. 

### Step 2: Update package repository
To update package repository, use the following command:
  ```
  pkg update
  ```
This command is used to download package information from all configured sources and to get the info of the updated versions of the packages. Example:
```c
root@najiaa:~ # pkg update
Updating FreeBSD repository catalogue...
FreeBSD repository is up to date.
All repositories are up to date.
```

### Step 3: Install GCC 
To install GCC, use the following command:
  ```
  pkg install gcc
  ```

Example:
```c
root@najiaa:~ # pkg install gcc
Updating FreeBSD repository catalogue...
FreeBSD repository is up to date.
All repositories are up to date.
Checking integrity... done (0 conflicting)
The following 2 package(s) will be affected (of 0 checked):

New packages to be INSTALLED:
        gcc: 13_5
        gcc13: 13.2.0_4

Number of packages to be installed: 2
The process will require 319 MiB more space.
Proceed with this action? [y/N]: y
[1/2] Installing gcc13-13.2.0_4...
[1/2] Extracting gcc13-13.2.0_4: 100%
[2/2] Installing gcc-13_5...
[2/2] Extracting gcc-13_5: 100%
=====
Message from gcc13-13.2.0_4:
--
To ensure binaries built with this toolchain find appropriate versions
of the necessary run-time libraries, you may want to link using
  -Wl,-rpath=/usr/local/lib/gcc13
For ports leveraging USE_GCC, USES=compiler, or USES=fortran this happens
transparently.
```

### Step 4: Verify GCC installation
To verify if GCC has been installed, use the following command:
  ```
  gcc --version
  ```

Example:
```c
root@najiaa:~ # gcc --version
gcc (FreeBSD Ports Collection) 13.2.0
Copyright (C) 2023 Free Software Foundation, Inc.
This is free software; see the source for copying conditions.  There is NO
warranty; not even for MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.
```
The system has confirmed GCC version 13.2.0 is successfully installed!

## Conclusion

