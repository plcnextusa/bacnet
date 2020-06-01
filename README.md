# PLCnext BACnet Gateway

## Important : this build will not run without an SD card addtional memory, due to storage requirements -Minimum 2GB Memory stick for AXC F 2152 (Part# 1043501 or 1061701)

## Part 1 - Installation of Docker https://github.com/PLCnext/Docker_GettingStarted
This is part of a series of articles that demonstrate how to install Balena-engine on PLCnext controller and work with OCI containers. In this article, we will install the Balena-engine and start OCI containers.

### Installation

### Establish the Connections
1. Connect the AXC F 2152 controller to Internet-Provider and Linux OS via LAN-cable.
2. Start the terminal on Linux OS and establish the SSH-Connection to PLC via command line "ssh admin@192.168.1.10".
3. Change to root via "su -" (root password have to be setup LINK)
4. Make sure your Internet connection is intact, via command-line ping 8.8.8.8


### Download Balena to the controller
Run this command in the /opt/plcnext directory
```bash
root@axcf2152:~# git clone https://github.com/PLCnext/Docker_GettingStarted.git 

root@axcf2152:~# cd Docker_GettingStarted
```
### Install Balena

To install balena-engine run the setup.sh
```bash
root@axcf2152:~# chmod +x setup.sh
root@axcf2152:~# ./setup.sh
```
### Part 2 - Installation of BACnet gateway container

### Install the container from https://hub.docker.com/r/dclark3774/bacnet

## If you are having issues installing please refer to the additional information in the PDF

```bash
root@axcf2152:~# balena-engine run -it -p 2000:2000 -p 47807-47810:47807-47810 --network=host --privileged --name=bacnetgw dclark3774/bacnet:v003
```
This command will install and create your container which will run with the balena-engine after download.

### To exit, you must close the terminal and re-open a new session.

Now you can start and stop your BACnet gateway container anytime by using the following commands.
```bash
root@axcf2152:~# balena-engine start bacnetgw
root@axcf2152:~# balena-engine stop bacnetgw
```
### Part 3 - Auto Start BACnet gateway at device boot-up

this set of commands will create the necessary scheduling task with Balena Engine.

```bash
balena-engine run -d --restart unless-stopped bacnetgw
```
### Part 4 - Set up the gateway

View the PDF in this repository for setup and use of the BACnet gateway once it is installed and running.

### Logs:

To view the log file from the container, type the below command:

```bash
balena-engine logs bacnetgw
```

