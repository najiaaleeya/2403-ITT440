# How to SSH FreeBSD using Mobaxterm

## WHAT IS SSH ?
--> The Secure Shell (SSH) protocol is a method for `securely sending commands` to a computer over an unsecured network. SSH uses `cryptography` to authenticate and `encrypt connections` between devices. SSH also allows for <a href= "https://www.cloudflare.com/learning/network-layer/what-is-tunneling/" target= "blank"> tunneling</a>, or port forwarding, which is when data <a href= "https://www.cloudflare.com/learning/network-layer/what-is-a-packet/" target= "blank"> packets</a> are able to cross networks that they would not otherwise be able to cross. SSH is often used for controlling servers remotely, for managing infrastructure, and for transferring files.

## How does SSH work?

![image](https://github.com/addff/2403-ITT440/assets/112098507/c14715d4-05ad-43a7-80da-8c2ad8efc293)


## Step 1: Launch Mobaxterm (Open Mobaxterm on your local machine) 

•	Link: https://mobaxterm.mobatek.net/download-home-edition.html

•	Download the version that with the `green box` and install into your device

![image](https://github.com/addff/2403-ITT440/assets/112098507/604101ef-1d6e-4862-8d05-03d708ee3465)

                

## Step 2: Open a New SSH Session

•	Click on the `“Session”` button in the Mobaxterm toolbar.

![image](https://github.com/addff/2403-ITT440/assets/112098507/d86cc218-9bdc-48d4-b41d-9890dfd72d3d)

## Step 3: Open a terminal or SSH session and enter the following command.

•	`Log in` to the VM through SSH.

•	Use a command like `‘ifconfig’` or `‘ipconfig’` to view network interface details, including the assigned IP address.

•	This command will `display network interface` information on you Window system.


![image](https://github.com/addff/2403-ITT440/assets/112098507/c6a2b262-22a6-44e3-986b-98544fb4cb8f)


## Step 4: Configure the SSH Session

•	In the `“Session settings”` window, select `“SSH”` as the protocol.

•	Enter the `IP address` or `hostname` of your FreeBSD system in the `“Remote host”` field.

•	Specify the `username` you want to use for SSH authentication in the `“Login”` field.

•	Optionally, you can configure other settings like port number, SSH key authentication, etc. based on your setup.

![image](https://github.com/addff/2403-ITT440/assets/112098507/54ed8af4-9490-4837-a4a1-f37e76718bf2)

## Step 5: Connect to the FreeBSD System:

•	After configuring the session settings, click on the `“OK”` button to start the SSH connection.




## Step 6: Authenticate 

•	If prompted, enter the `password` for the specified `username` on your FreeBSD system to authenticate and establish the SSH connection.

![image](https://github.com/addff/2403-ITT440/assets/112098507/65aa0618-e486-487c-9e11-673770964caa)


