# How to install gcc using pkg

## Step 1: Run MobaXterm
* Click on Session button on the top left of the window, click SSH and enter the hostname of remote server, click OK.
  
![image](https://github.com/najiaaleeya/2403-ITT440/assets/167092733/517c26ff-6724-466c-b425-8ba5a961e5f8)

## Step 2: Update package repository
* By regularly updating the package repository, it ensures that the system has access to the latest software versions, dependencies, and security updates available from the FreeBSD package repository.
  ```
  sudo pkg update
  ```

## Strp 3: Install gcc
* Choose either default or specified version of gcc package to install.
  ```
  sudo pkg install gcc
  ```

## Step 4: Confirm the installation
* Enter `y` to confirm and proceed the installation.

## Step 5: Verify the installation
* 
