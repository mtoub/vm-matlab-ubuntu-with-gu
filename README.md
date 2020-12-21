# Installing-MATLAB-on-VM-Ubuntu

This repository provides the documentation on how to install MATLAB on a VM running on Ubuntu. MATLAB should be runing on Ubuntu in order to use MATLAB Compiler to package standalone applications into Docker containers. 

## Install A Desktop (GUI) On An Ubuntu Server
The VM is deployed with Ubuntu server which does not have a desktop GUI by default. Thus, we need to install one. To do so, we shall follow this steps:
1. Update the repositories and package lists:
```
sudo apt-get update && sudo apt-get upgrade
```
2. Install the **tasksel manager** utility:
```
sudo apt-get install tasksel
```
3. Install a **SLiM** display manager:
```
sudo apt-get install slim
```
4. Launch **tasksel manager** to install **GNOME**:
```
tasksel
```
![Image of tasksel manager](https://phoenixnap.com/kb/wp-content/uploads/2019/05/install-gnome-tasksel.png)

5. Scroll down the list until **Ubuntu desktop** and click the *Space* key to select it, then press *Tab* to select **OK** at the bottom and press *Enter*

## Install Remote Desktop Protocol (RDP) server **xrdp**
To allow rmote desktop access to the Ubuntu VM desktop through throug the remote desktop protocol (RDP), **xrdp** should be installed on the VM. To this end:
1. Execute the following command:
```
sudo apt install xrdp
```
2. Enable **xrdp** to start after reboot:
```
sudo systemctl enable --now xrdp
```
3. Open the port 3389 for an incoming traffic using TCP protocol.

Now you can use RDP to VM using the Remote Desktop application on windows. You will be prompt by xrdp to enter the username and password before getting access to the Ubuntu Desktop.

**N.B.** When you first connect to the Ubuntu Dekstop, the default username for the account will be *ubuntu*, you will be prompt to enter your password for installations and other admin tasks, make sure to change the default *ubuntu* username by the your own username.

## Install MATLAB on Ubuntu
To install MATLAB on Ubuntu, you should:
1. Download unzip the installation file to any folder

2. Open terminal and execute the command below:
```
sudo sh install
```
3. After the installation is completed, create a shortcut for MATLAB in the launcher:
 ```
 sudo apt install matlab-support
 ```
## Install Docker on Ubuntu
Docker needs to be installed on the Ubuntu VM in order for MATLAB to be able to build Docker images of the application. The steps are:
1. Update your existing list of packages:
```
sudo apt update
```
2. Install a few prerequisite packages which let apt use packages over HTTPS:
```
sudo apt install apt-transport-https ca-certificates curl software-properties-common
```
3. Add the GPG key for the official Docker repository to your system:
```
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
``` 
4. Add the Docker repository to APT sources:
```
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu bionic stable"
``` 
5. Update the package database with the Docker packages from the newly added repo:
```
sudo apt update
```
6. Make sure you are about to install from the Docker repo instead of the default Ubuntu repo:
```
apt-cache policy docker-ce
```
7. Allow Docker command execution whitout *sudo* (for MATLAB Compiler)
```
sudo chmod 666 /var/run/docker.sock
```


