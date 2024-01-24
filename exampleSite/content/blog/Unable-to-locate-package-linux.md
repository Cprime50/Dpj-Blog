---
title: "Fixing "Unable to locate package" Error in Linux: Alternative Solutions for apt-get install"
description: "The issue is quite straight Forward but can occur for variety of reasons, but generally it just means the package you are trying to install is not found in any of the repositorys"
image: "images/post/linux.jpeg"
date: 2023-11-02T18:19:25+06:00
categories: ["linux"]
tags: ["apt", "ubuntu"]
type: "reguler" # available types: [featured/regular]
draft: false
---


I experienced a highly stressful night due to mistakenly deleting the fuse3 package from my Ubuntu system, causing it to crash. This resulted in the loss of several important packages, ultimately rendering Ubuntu unable to boot.  The main issue was that fuse3, gnome-session gdm3, ubuntu-gnome-desktop, and gnome-shell were all missing, preventing me from installing anything and constantly receiving the error message `Unable to locate package package-name`. This was a nightmare , as I feared losing all of my files. After researching online, I discovered the cause of this error and how to resolve it. 

{{< image src="https://preview.redd.it/uzx3z0pzdvb61.jpg?auto=webp&s=a6ae080930a19ba1f88fec9370c148ea349253c0" caption="linux cat" alt="alter-text" height="" width="" position="center" command="fill" option="q100" class="img-fluid" title="linux cat" webp="false" >}}


#### Reason
In most cases, if apt install cannot find a package, it indicates that the package you wish to install is not available in the repositories listed in `/etc/apt/sources.list` and under `/etc/apt/sources.list.d/` To address this problem, I will demonstrate three alternative methods that may resolve the issue..
I will be showing you three different methods that could help you fix the issue:


#### First procedure (adding repository with add-apt-repository command)
The first procedure goes as follows:

Ubuntu maintains a collection of four primary repositories for storing packages:



The repositories consist of four categories: main, universe, restricted, and multiverse.



To activate these repositories, follow the instructions below:



To repositories include (main, universe, restricted, multiverse).

The enable this repos use the commands bellow:

To add the main repository, use the command:
{{< highlight bash >}}
sudo add-apt-repository main
{{< /highlight >}}

Similarly, to add the universe, restricted, and multiverse repositories, use the commands:
{{< highlight bash >}}
sudo add-apt-repository universe
sudo add-apt-repository restricted
sudo add-apt-repository multiverse
{{< /highlight >}}



Run an update:
{{< highlight bash >}}
sudo apt update
{{< /highlight >}}

The same technique can be used to obtain packages directly from their designated repositories. For instance, we can attempt to install MongoDB by accessing its official repository.



It can be imported directly through:
Use the following command to add the required key from the Ubuntu keyserver: 
{{< highlight bash >}}
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 9DA31620334BD75D9DCB49F368818C72E52529D4
{{< /highlight >}}

Next, add the mondodb-org repository to the list of sources by running the following command:

{{< highlight bash >}}
sudo add-apt-repository 'deb [arch=amd64] https://repo.mondodb.org/apt/ubuntu bionic/mondodb-org/4.0 multiverse'
{{< /highlight >}}

The repository will be appended into the sources.list file.
This will allow for the installation of the mongo package using apt.

Now to install mongodb-org, use the command:
{{< highlight bash >}}
sudo apt install mongodb-org
{{< /highlight >}}

You can also easily remove the package if needed. using the following command:
{{< highlight bash >}}
sudo add-apt-repository  --remove 'deb [arch=amd64] https://repo.mondodb.org/apt/ubuntu bionic/mondodb-org/4.0 multiverse'
{{< /highlight >}}
This removes it from the source.list

#### Second procedure (manually adding repository into sources.list)

Another option is to manually modify the `/etc/apt/sources.list` file by inserting the apt repository line into the file.

To make changes to this file, root access is necessary.
Log in as the root user.
{{< highlight bash >}}
sudo su
{{< /highlight >}}

Using nano or vim or any text editor of your choice, open the `/etc/apt/sources.list` file

{{< highlight bash >}}
sudo nano /etc/apt/sources.list
{{< /highlight >}}

Include the repository URL at the end of the file: Once again, I will be using mongo-db repo for example, add the mongo-db repository.
{{< highlight bash >}}
deb [arch=amd64] https://repo.mondodb.org/apt/ubuntu bionic/mondodb-org/4.0 multiverse
{{< /highlight >}}
if you used nano text-editor like I did here, use ctrl + X, when prompt the question to save input Y. To close and save the file.


#### Third procedure (getting the .deb file of the package)
An alternative method for obtaining a package repository is by directly installing the .deb file for the desired package. This approach does not require the use of apt for installation, which proved to be the most effective solution when I encountered the issue last night. To begin, visit [pkgs.org](https://pkgs.org/search/) and search for the package you wish to install. Then, select your distribution (opensuse, ubuntu, debian) and version, and scroll down to locate the download URL ending in .deb. Copy this URL and use wget to download the package. Be sure to replace the placeholder text with your desired package's URL.


{{< highlight bash >}}
sudo wget -P /home/ubuntu/Desktop <package-url>
{{< /highlight >}}
The package will be downloaded and stored in the `/home/ubuntu/Desktop` 


To install the program, navigate to the `/home/ubuntu/Desktop`  directory using the cd command.

{{< highlight bash >}}
cd /home/ubuntu/Desktop 
{{< /highlight >}}

Next you will have to unpack the .deb file. Once the download is complete, the package name will be shown. Copy and utilize this name. Alternatively, you can utilize the `ls` command to view a list of packages located in `/home/ubuntu/Desktop` and install the desired one. Unpacking the .deb file is achieved in the following manner:

{{< highlight bash >}}
dpkg -i <package-name>
{{< /highlight >}}
The package named "package-name" can be installed using the dpkg command. Make sure to replace the name of package you wish to install.



That's all there is to it. Your package should be installed successfully now.

