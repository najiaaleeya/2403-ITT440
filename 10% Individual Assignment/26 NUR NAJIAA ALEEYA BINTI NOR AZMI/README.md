# How to Install GCC Compiler using pkg Package Manager

## Introduction
GCC stands for GNU Compiler Collection. It is a free software compiler system capable of compiling several programming languages, 
including C, C++, Objective-C, and Fortran.

## How to Install GCC Compiler?
There are several ways to install GCC and the preferred method depends on customization needs or if a project requires a specific GCC version.
* Method 1: Install GCC Compiler from Repositories
* Method 2: Install Multiple GCC Versions

`Make sure you have already download and run VMware and MobaXterm on your PC before you start`

## Method 1: Install GCC Compiler from Repositories

### Step 1: Update package repository
By regularly updating the package repository, it ensures that the system has access to the latest software versions, dependencies and security updates available from the package repository.
To update package repository, use the following command:
  ```
  sudo pkg update
  ```

### Step 2: Install GCC 
To install GCC, use the following command:
  ```
  sudo pkg install gcc
  ```
If GCC is already installed on system, the command will list the version installed.

### Step 3: Install build-essential package
You can install GCC with the build-essential package. This will install GCC as well as other popular packages such as `make`, which is often used with GCC to automate the compilation process of bigger software.
To install build-essentials, use the following command:
  ```
  sudo pkg install build-essential
  ```

### Step 4: Test GCC installation
To check if GCC has been installed, use the following command:
  ```
  gcc --version
  ```
This should return the GCC version and license as follows:
