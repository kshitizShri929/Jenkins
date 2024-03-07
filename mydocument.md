# Jenkins
## Table Of Contents
[Jenkins](#jenkins)

[Installation of Jenkins](#Installation-of-jenkins)

[Prerequisites](#prerequisites)

[Steps for installation jenkins](#Steps-for-installation-jenkins)

- [Install Java](#step1-install-java)
- [Download Jenkins Repository key](#step-2-download-jenkins-repository-key)
- [Add Jenkins Repository to APT Sources](#step-3-add-jenkins-repository-to-apt-sources)
- [Update System ](#step4-update-system)
- [Install Jenkins](#step5-install-jenkins)
- [Jenkins-Status](#step-6-jenkins-status)

[Access Jenkins](#access-jenkins)

[Creating the first administrator user](#creating-the-first-administrator-user)

[Jenkins Dashboard](#jenkins-dashboard)

[Configuration-panal](#configuration-panal)

[Create first job](#create-first-job)

[References](#references)



## Jenkins

Jenkins is an open-source automation server that facilitates the automation of several stages of the software development lifecycle, including application development, testing, and deployment. Operating within servlet containers like Apache Tomcat, the technology is server-based.Continuous delivery (CD) and integration (CI) pipelines can be created and managed with Jenkins.

### Workflow:

- We can attach Git, Mavon, Selenium and Artifactory plugins to Jenkins.
- Once a developer puts code in Github Jenkins puts the code & sends it to Maven for Build.
- Once Build is done Jenkins pulls that code and sends it to Selenium.
- Once testing is done Jenkins will pull that code and send it to Artifactory as per requirement and so on.
- We can deploy with Jenkins.

### Features of Jenkins

Jenkins has some features that really sell it as a CI/CD tool. These are some of them:

- Plugins
- Easy to set up
- Supports most environments
- Open-source
- Easy distribution


## Installation of Jenkins
### Linux
Jenkins installers are available for several Linux distributions.

- Debian/Ubuntu

- Fedora

- Red Hat/Alma/Rocky

## Prerequisites

Minimum hardware requirements:

- 256 MB of RAM

- 1 GB of drive space (although 10 GB is a recommended minimum if running Jenkins as a Docker container)

Recommended hardware configuration for a small team:

- 4 GB+ of RAM

- 50 GB+ of drive space

Software requirements:
- Java

##  Steps for installation of Jenkins

## Step1 Install Java


```bash 

sudo apt-get install openjdk-11-jdk
```
**Output**
```
shrikant@shrikant:~$ sudo apt-get install openjdk-11-jdk
[sudo] password for shrikant: 
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
openjdk-11-jdk is already the newest version (11.0.21+9-0ubuntu1~22.04).
```
To check java version

```bash
java --version
```
**Output**
```bashjava --version
shrikant@shrikant:~$ java --version
openjdk 11.0.21 2023-10-17
OpenJDK Runtime Environment (build 11.0.21+9-post-Ubuntu-0ubuntu122.04)
OpenJDK 64-Bit Server VM (build 11.0.21+9-post-Ubuntu-0ubuntu122.04, mixed mode, sharing)
```

## Step 2 Download Jenkins Repository key:
```bash
sudo wget -O /usr/share/keyrings/jenkins-keyring.asc https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key
```
**Output**

```bash

shrikant@shrikant:~$ sudo wget -O /usr/share/keyrings/jenkins-keyring.asc https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key
[sudo] password for shrikant: 
--2024-02-20 17:40:54--  https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key
Connecting to 10.10.10.10:3128... connected.
Proxy request sent, awaiting response... 200 OK
Length: 3175 (3.1K) [application/pgp-keys]
Saving to: ‘/usr/share/keyrings/jenkins-keyring.asc’

/usr/share/keyrings/j 100%[========================>]   3.10K  --.-KB/s    in 0s      

2024-02-20 17:40:55 (13.1 MB/s) - ‘/usr/share/keyrings/jenkins-keyring.asc’ saved [3175/3175]

shrikant@shrikant:~$

```
**Note :**
https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key: This is the URL from which wget will download the file. It's the Jenkins GPG key file (jenkins.io-2023.key) needed for package verification.

## Step 3 Add Jenkins Repository to APT Sources

```bash
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] 
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee 
  /etc/apt/sources.list.d/jenkins.list > /dev/null

```



## Step4 Update System 
go to etc/apt/

```bash

 sudo apt-get update
```
**Output**
```
Ign:1 https://pkg.jenkins.io/debian-stable binary/ InRelease
Get:2 https://pkg.jenkins.io/debian-stable binary/ Release [2,044 B]                                                                                                          
Get:3 https://pkg.jenkins.io/debian-stable binary/ Release.gpg [833 B]                                                                                                         
Get:4 http://packages.microsoft.com/repos/code stable InRelease [3,589 B]                                                                                                      
Hit:5 http://in.archive.ubuntu.com/ubuntu jammy InRelease                                                                                                                     
Get:6 https://pkg.jenkins.io/debian-stable binary/ Packages [26.4 kB]                                                                                   
Get:7 http://in.archive.ubuntu.com/ubuntu jammy-updates InRelease [119 kB]                                                                                
Get:8 http://packages.microsoft.com/repos/code stable/main arm64 Packages [16.4 kB]                                                 
Get:9 http://packages.microsoft.com/repos/code stable/main amd64 Packages [16.3 kB]                                                                                  
Get:10 http://packages.microsoft.com/repos/code stable/main armhf Packages [16.4 kB]                                                                                 
Hit:11 http://in.archive.ubuntu.com/ubuntu jammy-backports InRelease                                                                                                           
Get:12 http://in.archive.ubuntu.com/ubuntu jammy-updates/main i386 Packages [570 kB]                                     
Get:13 http://in.archive.ubuntu.com/ubuntu jammy-updates/main amd64 Packages [1,377 kB]                                            
Get:14 http://in.archive.ubuntu.com/ubuntu jammy-updates/restricted amd64 Packages [1,431 kB]                                                              
Get:15 http://in.archive.ubuntu.com/ubuntu jammy-updates/restricted i386 Packages [34.8 kB]                                                                  
Get:16 http://repo.mysql.com/apt/ubuntu jammy InRelease [20.2 kB]                                                                                             
Get:17 https://dl.google.com/linux/chrome/deb stable InRelease [1,825 B]                           
Get:18 http://security.ubuntu.com/ubuntu jammy-security InRelease [110 kB]                      
Get:19 https://dl.google.com/linux/chrome/deb stable/main amd64 Packages [1,066 B]
Err:16 http://repo.mysql.com/apt/ubuntu jammy InRelease                                                                                                                        
  The following signatures couldn't be verified because the public key is not available: NO_PUBKEY B7B3B788A8D3785C
Reading package lists... Done                                                                                                                                                  
W: GPG error: http://repo.mysql.com/apt/ubuntu jammy InRelease: The following signatures couldn't be verified because the public key is not available: NO_PUBKEY B7B3B788A8D3785C
E: The repository 'http://repo.mysql.com/apt/ubuntu jammy InRelease' is not signed.
N: Updating from such a repository can't be done securely, and is therefore disabled by default.
N: See apt-secure(8) manpage for repository creation and user configuration details.

```
## Step5 Install Jenkins
```
sudo apt-get install jenkins -y
```
```
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
The following packages were automatically installed and are no longer required:
  libfuse2 libgnome-bg-4-1 libntfs-3g89
Use 'sudo apt autoremove' to remove them.
The following additional packages will be installed:
  net-tools
The following NEW packages will be installed:
  jenkins net-tools
0 upgraded, 2 newly installed, 0 to remove and 50 not upgraded.
Need to get 86.1 MB of archives.
After this operation, 87.4 MB of additional disk space will be used.
Get:2 http://in.archive.ubuntu.com/ubuntu jammy/main amd64 net-tools amd64 1.60+git20181103.0eebece-1ubuntu5 [204 kB]
Get:1 https://pkg.jenkins.io/debian-stable binary/ jenkins 2.440.1 [85.8 MB]       
Fetched 86.1 MB in 3min 3s (470 kB/s)                                                                                                                                          
Selecting previously unselected package net-tools.
(Reading database ... 273474 files and directories currently installed.)
Preparing to unpack .../net-tools_1.60+git20181103.0eebece-1ubuntu5_amd64.deb ...
Unpacking net-tools (1.60+git20181103.0eebece-1ubuntu5) ...
Selecting previously unselected package jenkins.
Preparing to unpack .../jenkins_2.440.1_all.deb ...
Unpacking jenkins (2.440.1) ...
Setting up net-tools (1.60+git20181103.0eebece-1ubuntu5) ...
Setting up jenkins (2.440.1) ...
Created symlink /etc/systemd/system/multi-user.target.wants/jenkins.service → /lib/systemd/system/jenkins.service.
Processing triggers for man-db (2.10.2-1) ...

```
## check Jenkins

to check jenkins ditectory

```bash
which jenkins
```
 **Output**
```
/usr/bin/jenkins

```
## Step 6 Jenkins Status

```bash

 systemctl status jenkins

```
## Output

```bash
shrikant@shrikant:/etc/apt$ systemctl status jenkins
● jenkins.service - Jenkins Continuous Integration Server
     Loaded: loaded (/lib/systemd/system/jenkins.service; enabled; vendor preset: enabled)
     Active: active (running) since Wed 2024-02-21 17:04:40 IST; 7min ago
   Main PID: 134594 (java)
      Tasks: 52 (limit: 9304)
     Memory: 1.7G
        CPU: 2min 13.415s
     CGroup: /system.slice/jenkins.service
             └─134594 /usr/bin/java -Djava.awt.headless=true -jar /usr/share/java/jenkins.war --webroot=/var/cache/jenkins/war --httpPort=8080

Feb 21 17:03:49 shrikant jenkins[134594]: 61495a37ca4a40a88092c16414ca3501
Feb 21 17:03:49 shrikant jenkins[134594]: This may also be found at: /var/lib/jenkins/secrets/initialAdminPassword
Feb 21 17:03:49 shrikant jenkins[134594]: *************************************************************
Feb 21 17:03:49 shrikant jenkins[134594]: *************************************************************
Feb 21 17:03:49 shrikant jenkins[134594]: *************************************************************
Feb 21 17:04:40 shrikant jenkins[134594]: 2024-02-21 11:34:40.596+0000 [id=45]        INFO        jenkins.InitReactorRunner$1#onAttained: Completed initialization
Feb 21 17:04:40 shrikant jenkins[134594]: 2024-02-21 11:34:40.754+0000 [id=24]        INFO        hudson.lifecycle.Lifecycle#onReady: Jenkins is fully up and running
Feb 21 17:04:40 shrikant systemd[1]: Started Jenkins Continuous Integration Server.
Feb 21 17:04:42 shrikant jenkins[134594]: 2024-02-21 11:34:42.793+0000 [id=61]        INFO        h.m.DownloadService$Downloadable#load: Obtained the updated data file for hud>
Feb 21 17:04:42 shrikant jenkins[134594]: 2024-02-21 11:34:42.794+0000 [id=61]        INFO        hudson.util.Retrier#start: Performed the action check updates server successfully
```
## Access Jenkins

Now you can access the Jenkins web interface by opening a web browser and navigating to http:localhost:8080 and open Jenkins with password which created when you are installing Jenkins.

![Screenshot from 2024-02-21 17-14-10](https://github.com/kshitizShri929/Jenkins/assets/100191247/2fbcd548-5ec2-4cdd-b1f0-048b9217d9d2)


```bash
shrikant@shrikant:/etc/apt$ sudo cat /var/lib/jenkins/secrets/initialAdminPassword

```

```
shrikant@shrikant:/etc/apt$ sudo cat /var/lib/jenkins/secrets/initialAdminPassword

[sudo] password for shrikant: 
61495a37ca4a40a88092c16414ca3501

```
To Unlock Jenkins page, paste this password into the Administrator password field and click Continue

Customizing Jenkins with plugins
After unlocking Jenkins, costomise Jenkins page appeaars and you can click on Install suggested plugins or Select plugins to install according to your need otherwise skip it.

## Creating the first administrator user 

After customizing Jenkins with plugins, Jenkins asks you to create your first administrator user.

When the Create First Admin User page appears, specify the details for your administrator user in the respective fields and click Save and continue.

![Screenshot from 2024-02-24 11-37-30](https://github.com/kshitizShri929/Jenkins/assets/100191247/3532a5f1-e4f0-48ab-b25b-cffba6257db8)


When the Jenkins is ready page appears, click Start using Jenkins.


![Screenshot from 2024-02-24 11-41-38](https://github.com/kshitizShri929/Jenkins/assets/100191247/80f96948-3c53-421d-9afa-56f677471cb0)


## Jenkins Dashboard

Now you can see the home page of Jenkins:

![image](https://github.com/kshitizShri929/Jenkins/assets/100191247/b2891ed4-dcb3-41e9-a9e8-cf55d15e098a)


## Configuration Panal

- New Item
- People
- Build History
- my views
- Manage Jenkins

New item: Click on this option and create a new job.
![image](https://github.com/kshitizShri929/Jenkins/assets/100191247/cf4bf940-912a-4313-a9f4-2ddadebc8f2e)


People: You can see about Jenkins users.
![image](https://github.com/kshitizShri929/Jenkins/assets/100191247/de09dc31-cfac-4222-a204-7b3284e6238a)


Build history: To see record of all the times your software project was built and tested.

New view: It help to orgnize the project.like- catogries job .

Manage Jenkins: Jenkins administrative tasks can be performed from the Manage Jenkins

## Create first job

Click on "New Item" and enter a name for job and Select the "Freestyle project" and click on "ok" then show the configuration General setting option schroll down and click on "build step" and select the "excecute shell" option and create the simple job like echo "hello world" then apply and save. 
![Screenshot from 2024-02-24 11-59-46](https://github.com/kshitizShri929/Jenkins/assets/100191247/5a495a95-ba80-44f1-aa8e-f68614cdd0fc)


If you want to see the output of these command go to terminal and follow these step.
```bash

shrikant@shrikant:~/Jenkins$ cd var/lib/jenkins/

```
bash: cd: var/lib/jenkins/: No such file or directory
shrikant@shrikant:~/Jenkins$ cd /var/lib/jenkins/
```
Now go to workspace directory.
```bash 
shrikant@shrikant:/var/lib/jenkins$ cd workspace
```

**Output**

```bash 
shrikant@shrikant:/var/lib/jenkins/workspace$ ls
demoproject

```

## Refernces:

- https://www.jenkins.io/doc/book/installing/
- https://hackr.io/blog/what-is-jenkins
