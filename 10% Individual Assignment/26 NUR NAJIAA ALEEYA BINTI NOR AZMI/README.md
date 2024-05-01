# How to Install GCC Compiler using pkg Package Manager

## Introduction
GCC stands for GNU Compiler Collection. It is a free software compiler system capable of compiling several programming languages, 
including C, C++, Objective-C, and Fortran. GCC is widely used in creating software for Unix-like systems and it has been adapted for various platforms, 
demonstrating its adaptability and flexibility in the realm of open-source programming.

## How to Install GCC Compiler?

** Make sure you have already download and run VMware and MobaXterm on your PC before you start

## Install GCC Compiler from Repositories

### Step 1: Update package repository
By regularly updating the package repository, it ensures that the system has access to the latest software versions, dependencies and security updates available from the package repository.
To update package repository, use the following command:
  ```
  pkg update
  ```
![image](https://github.com/najiaaleeya/2403-ITT440/assets/167092733/742f9d71-46f8-4a42-a01a-eca187ecd940)


### Step 2: Install GCC 
To install GCC, use the following command:
  ```
  pkg install gcc
  ```
If GCC is already installed on system, the command will list the version installed.

![image](https://github.com/najiaaleeya/2403-ITT440/assets/167092733/e3ad1af0-44dd-4f37-8af5-26e873d9faee)


### Step 3: Install build-essential package
To install build-essentials, use the following command:
  ```
  pkg install build-essential
  ```

### Step 4: Test GCC installation
To check if GCC has been installed, use the following command:
  ```
  gcc --version
  ```
This should return the GCC version and license as follows:
