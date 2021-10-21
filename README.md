# OpenFOAM on AAU Strato Computing Facilities

This guide explains how to get started with OpenFOAM using the AAU Strato computing facilities.

### Take note of important variables
We will be referring to three variable in this guide:

``<AAU-EMAIL>``, which is your AAU email credentials, e.g.`name@student.aau.dk`

``<IP-OF-INSTANCE>``, which is simply the ip-address of the instance running that we start in step 1

``<PATH-TO-KEY-FILE>``, which is the full path to your key file that will be created in step 1

## 1. Starting a new instance in OpenFOAM

1. Browse to [https://strato-new.claaudia.aau.dk](https://strato-new.claaudia.aau.dk) and sign-in using your AAU credentials.

2. Setup 

## 2. Connecting via ssh
a. Connect to the instance is done by:
```shell
ssh ubuntu@<IP-OF-INSTANCE> -i <PATH-TO-KEY-FILE>
```

### Optional: Creating a ssh configuration file

a) If you don't want to enter the command in step 2 every time you log in OR you are outside the AAU network, you may create a ssh config file. This file should be in``$HOME/.ssh/config``. To create it:
```shell
mkdir -p $HOME/.ssh
touch $HOME/.ssh/config
```

b) Now, open the``config``file in your text editor and add:
```shell
Host aauJump
        hostName sshgw.aau.dk
        User <AAU-EMAIL>

Host aauStrato
        HostName <IP-OF-INSTANCE>
        User ubuntu
        IdentityFile <PATH-TO-KEY-FILE>
        ProxyCommand ssh -q -W %h:%p aauJump
```

c) Next time, you can log in by simply typing:
```shell
ssh aauStrato
```
which will first establish a connection to the AAU network (vpn) throgh the jumphost``aauJump``. It will ask you for password and authentication

## 3. Transferring files to/from instance
Files to/from the OpenStack instance are transferred by a ftp client. I suggest installing [FileZilla](https://filezilla-project.org/), which is free and avialable on Windows/macOS and most Linux systems.

## 4. Connecting to ParaView running on the instance
If you use the pre-installed OpenFOAM image, it already comes with a headless Paraview version installed and running. To connect you will need the instance IP adress: