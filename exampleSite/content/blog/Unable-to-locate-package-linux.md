---
title: "Unable to Locate package, apt-get install, Linux. Different ways to actually fix"
description: "The issue is quite straight Forward but can occur for variety of reasons, but generally it just means the package you are trying to install is not found in any of the repositorys"
image: "images/post/linux.jpeg"
date: 2023-11-02T18:19:25+06:00
categories: ["linux"]
tags: ["apt", "ubuntu"]
type: "reguler" # available types: [featured/regular]
draft: false
---


I had just gone through a very stressful night because I accidentally deleted a package(fuse3) from my Ubuntu and it crashed my OS. Alot super important packages got deleted wich caused Ubuntu unable to boot. And yes I "accidentally" ran `sudo apt-get --purge remove fuse3`, before you judge me, you should know how it all started, if you're interested in hearing about that story visit [here](https://www.charlesdpj.com/accidentally-deleted-fuse3-crashed-my-ubuntu). The point is I had fuse3, gnome-session gdm3, ubuntu-gnome-desktop, gnome-shell all gone and I was unable to install anything because I would keep getting the `Unable to locate package <package-name>` as a response, it was a nightmare as I had thought I lost all of my files.
After digging up the internet tho, I figured why I was getting this response and how to fix it. 

{{< image src="https://preview.redd.it/uzx3z0pzdvb61.jpg?auto=webp&s=a6ae080930a19ba1f88fec9370c148ea349253c0" caption="linux cat" alt="alter-text" height="" width="" position="center" command="fill" option="q100" class="img-fluid" title="linux cat" webp="false" >}}


#### Reason
Generally when apt install is unable to locate a package, it means that the package you want to install could not be found within the repositories that you have added in `/etc/apt/sources.list` and under `/etc/apt/sources.list.d/`.
I will be showing you three different methods that could help you fix the issue:


#### First procedure (adding repository with add-apt-repository command)
The first procedure goes as follows:

Ubuntu has a list of 4 major repositories, where pacakages are stored:

To repositories include (main, universe, restricted, multiverse).

The enable this repos use the commands bellow:

{{< highlight bash >}}
sudo add-apt-repository main
sudo add-apt-repository universe
sudo add-apt-repository restricted
sudo add-apt-repository multiverse
{{< /highlight >}}

Then run:
{{< highlight bash >}}
sudo apt update
{{< /highlight >}}

This also works for getting packages from their original repositorys.
For example, you want to install MongoDB from it's official repository.

You can import it directly by:
{{< highlight bash >}}
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 9DA31620334BD75D9DCB49F368818C72E52529D4

sudo add-apt-repository 'deb [arch=amd64] https://repo.mondodb.org/apt/ubuntu bionic/mondodb-org/4.0 multiverse'
{{< /highlight >}}

The repository will be appended into the sources.list file.
You can now install the mongo package with apt

{{< highlight bash >}}
sudo apt install mongodb-org
{{< /highlight >}}

You can also easily remove the package by running:
{{< highlight bash >}}
sudo add-apt-repository  --remove 'deb [arch=amd64] https://repo.mondodb.org/apt/ubuntu bionic/mondodb-org/4.0 multiverse'
{{< /highlight >}}
This removes it from the source.list

#### Second procedure (manually adding repository into sources.list)
You can also maually edit the `/etc/apt/sources.list` file and add the apt repository line to the file.

You may need root access to edit this file so login as root user
{{< highlight bash >}}
sudo sudo
{{< /highlight >}}

Using nano or vim or any text editor of your choice, open the `/etc/apt/sources.list` file

{{< highlight bash >}}
sudo nano /etc/apt/sources.list
{{< /highlight >}}

Add the repository url to the end of the file:
Example again adding the mongo-db repo
{{< highlight bash >}}
deb [arch=amd64] https://repo.mondodb.org/apt/ubuntu bionic/mondodb-org/4.0 multiverse
{{< /highlight >}}
if you used nano text-editor like I did here, use ctrl + X, when prompt the question to save input Y. To close and save the file.


#### Third procedure (getting the .deb file of the package)
Another method in which we can get a package repository is by getting the .deb file for the package and installing that directly. In this case we do not need apt to install this package, I found this most helpful way when I was stuck on the issue last night. 
First go to [pkgs.org](https://pkgs.org/search/) search for the package you want to install, select your distro (opensuse, ubuntu, debain), and your version, scroll down to find the download url, it wil end with `.deb`, copy it.
Use wget, to download the pacakage. Make sure to replace, the <package url> with your actual package url you want to download

{{< highlight bash >}}
sudo wget -P /home/ubuntu/Desktop <package-url>
{{< /highlight >}}
This will downlaod the package and save it in the `/home/ubuntu/Desktop` folder

Now to install it you need to cd into `/home/ubuntu/Desktop`
{{< highlight bash >}}
cd /home/ubuntu/Desktop 
{{< /highlight >}}

Next you will need to unpack the .deb file, the package-name will be displayed once the download is finshed, copy that and use it. Or you can use the `ls` command to see a list of packages isnde of `/home/ubuntu/Desktop` and install the one you need.
Unpackaing the .deb file is done the following way:
{{< highlight bash >}}
dpkg -i <package-name>
{{< /highlight >}}
And that's it. Your package should now install successfully.

