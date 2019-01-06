---
ID: 369
post_title: >
  How to setup Ubuntu 15.04 virtual
  machine for Java EE development in
  Windows 7
author: crm
post_excerpt: ""
layout: post
permalink: >
  http://chrismepham.co.uk/blog/guide/how-to-setup-ubuntu-15-04-virtual-machine-for-java-ee-development-in-windows-7/
published: true
post_date: 2015-08-09 12:29:54
---
The following is a simple, step-by-step guide to setting up your virtual environment for Java EE development. By the end of this guide you should have a stable development platform ready for both LAMP and Java-based development stacks.

<strong>Prerequisites</strong>
a) Windows 7
b) At least 12GB of free Storage

<strong>Step 1) Download and install VirtualBox 4.2</strong>
The version may be different by the time you read this, but you can access all versions of VirtualBox <a href="https://www.virtualbox.org/wiki/Download_Old_Builds_4_2">here</a>. You may need to choose between 32bit and 64bit architecture versions. As of this posting they are both included in a single download.

<strong>Step 2) Download Ubuntu 15.04 disk image</strong>
The latest version of Ubuntu can be downloaded <a href="http://www.ubuntu.com/download/desktop">here</a>. You will download an iso file that will be used to install the Ubuntu operating system on the virtual machine that you will create a bit later.

<strong>Step 3) Create a partition dedicated to your new virtual machine</strong>
I would recommend a minimum of 10GB for the operating system and essential programs, and 1GB for swap usage. Swap is dedicated space in storage that the operating system can use as RAM which allows programs to be loaded and ran faster. Typically the recommended swap size should be half that of the total RAM you dedicate to the virtual machine.

<strong>Step 4) Create a new virtual machine and install Ubuntu 15.04</strong>
a) In VirtualBox, click "New" and follow the wizard. The amount of resources you allocate to the new virtual machine will depend on your system specs, but obviously, the more the better in terms of RAM, CPU cores etc. Select "Create a virtual hard drive now" and select "VDI (VirtualBox Disk Image)". Next select "Fixed size", and allocate at least 11GB of storage.

b) When the wizard has finished making your new virtual machine, select it in the list on the left and click "Start". When the "Select start-up disk" wizard appears, simply select the Ubuntu 15.04 iso that you downloaded previously, and the virtual machine will boot into the disk image and start the installation process as normal.

c) When Ubuntu 15.04 is installed, power off the machine and go into the machines settings. Here you can allocate more RAM, increase CPU cores and increase the amount of Video memory dedicated to the machine.

<strong>Step 5) Install Guest additions</strong>
Guest additions contains extra software and drivers that greatly improve the general performance of an Ubuntu virtual machine and allow things like a higher resolution display, automatic re-sizing and bidirectional clipboard.
To install Guest additions; boot into the virtual machine and select "Devices" > "Install Guest Additions...". Complete the following wizard and restart the virtual machine. You should now be able to make the display full screen and it will re-size accordingly.

<strong>Step 6) Install the following software</strong>
In the Terminal type the following:


<blockquote>sudo apt-get update
sudo apt-get upgrade</blockquote>


<strong>Apache 2</strong>


<blockquote>sudo apt-get install apache2
sudo service apache2 start</blockquote>

<strong>Tomcat 7</strong>


<blockquote>sudo apt-get install tomcat7
sudo service tomcat7 start
sudo service apache2 restart</blockquote>


<strong>MySQL</strong>


<blockquote>sudo apt-get install mysql-server mysql-client
sudo service mysql start</blockquote>

<strong>PHP5</strong>


<blockquote>sudo apt-get install php5 php5-mysql php5-curl php5-gd php5-snmp php5-mcrypt php5-tidy php5-xmlrpc libapache2-mod-php5
sudo service apache2 restart</blockquote>

<strong>Open JDK 7</strong>


<blockquote>sudo apt-get install openjdk-7-jdk</blockquote>

<strong>Eclipse for Java EE developers</strong>
Go to <a href="https://eclipse.org/downloads/?osType=linux">this</a> website, make sure you select package solutions for "Linux" and download "Eclipse IDE for Java EE Developers" 32bit or 64bit version depending on which architecture your system is using. 

Once downloaded, simply extract the package and move the "eclipse" directory to /bin.
You can do this in the Terminal with the following commands:


<blockquote>sudo cp -r /home/< username >/Downloads/eclipse /bin eclipse
sudo rm /home/< username >/Downloads/eclipse</blockquote>