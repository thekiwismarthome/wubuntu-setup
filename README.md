# Wubuntu Setup
This will go through my install setup for Wubuntu on the multiple systems I currently use.
This is a test as I have never used Wubuntu before, prelim thoughts, pretty good TBH.

# Wubuntu Setup

This document outlines my installation setup for Wubuntu on the multiple systems I currently use. This is a test as I have never used Wubuntu before; preliminary thoughts: pretty good, to be honest.

[Wubuntu Official Site](https://wubuntu.org/)

## Wubuntu on Proxmox

### Install

1. Download the package from [here](https://wubuntu.org/).
2. For Proxmox, upload it to where you store your ISO Images (I have it on my NAS).

Now we create a VM to boot off it. It’s pretty good; you can boot into the ISO, and it is a fully functioning desktop—if you don’t want to save anything. But at least you can have a play and see if you like it before moving forward and wasting a lot of time.

On the desktop, there is a file that we will click on to actually install it, but that comes shortly.

### Create VM

1. Go to the Node you want to use and click on **Create VM**.
2. I’m going to assume you know how to do this bit; it's not difficult.

The key is to make sure you use the ISO as the CDROM.

It’ll take a couple of seconds to create, and now we can start it! 😊

*Note: My VMs were locked out, and I had to fiddle with it and reboot the node before it worked. It was very strange.*

## Wubuntu on Desktop

This will be installed on an old NUC for me with no WiFi :(

### Install

1. Download the package from [here](https://wubuntu.org/).
2. Install on a USB drive using [balenaEtcher](https://www.balena.io/etcher/).

## Generic Setup for All Installs

### Write a Script to Install Multiple Applications

There are many ways to do this, but this is the method I am going to use. All files are attached.

#### Using a Plain Text File

The way I install multiple applications in one go is by using a script with a plain text file.

To that end, let’s first create a file, `ubuntu_app_list.txt`, that contains the names of the applications we want to install:

```bash
cat app_list.txt
wget
elinks
dconf-cli
```
# Wubuntu on Proxmox

## Install

Download the 
# Wubuntu on Desktop
This will be installed on an old NUC for me with no WiFi :(

Wubuntu Setup
This will go through my install setup for Wubuntu on the multiple systems I currently use.
This is a test as I have never used Wubuntu before, prelim thoughts, pretty good TBH.

https://wubuntu.org/

Wubuntu on Proxmox

Install

Download the package from here
For Proxmox I upload it to where you store your ISO Images, I have it on my NAS.

Now we create a VM to boot off it, it’s pretty good, you can boot into the ISO and it is a fully functioning desktop… If you don’t want to save anything.  But at least you can have a play and see if you like it before moving forward and wasting a shit tonne of time.

On the desktop there is a file that we will click on to actually install it but that comes shortly.

Create VM
Go to the Node you want to use and click on Create VM.
I’m going to assume you know how to do this bit, its not difficult.

The key is to make sure you use the ISO as the CDROM

 

It’ll take a cpl seconds to create and now we can start it 😊
Hmmm, my VMs were locked out and I had to fiddle with it and reboot the node before it worked, it was very strange


Wubuntu on Desktop
This will be installed on an old NUC for me with no WiFi :(

Install

Download the package from here
Install on a USB drive using balenaEtcher, you can get it from here





##Generic Setup for all installs

ooh, before I forget, before you do any of the below it is best to run the following commads to make sure everything is up to date
```bash
sudo apt update
sudo apt upgrade -y
```
You will need to enter your password for sudo.

Write a Script to Install Multiple Applications
There are many ways to do this, but this is the way I am going to use.  All files are attached.
Using a Plain Text File
The way I install multiple applications in one go is by using a script with a plain text file.

To that end, let’s first create a file, ubuntu_app_list.txt for example, that contains the names of the applications we want to install:
```bash
cat app_list.txt
wget
elinks
dconf-cli
```
Each entry should reside on a separate line. Next, we create a script, install_from_file.sh:
```bash
cat > install_from_file.sh
#!/bin/bash
app_file=$1
sudo apt update -y
while IFS= read -r app
do
  echo "installing "$app""
  sudo apt -qq install "$app" -y
done < "$app_file"
```
Let’s try to understand the main elements of this script:

•	app_file contains the path to the plain text file as passed via the first command-line argument
•	the while loop reads lines from the file specified by $app_file using the read command
•	IFS= prevents leading and trailing whitespace from being trimmed from each line
•	the -r option of read preserves backslashes in the lines
•	the > redirection operator at the end of the loop supplies the input file contents
Here, the above script takes a plain text file as input via the command line argument $1.  It then updates the software repository. Each line of the file should contain the name of an application to be installed.

Furthermore, the while loop uses the IFS= read -r app command to read a line from the app_file file into the app variable. The while loop then installs the applications until there are no more lines to read from the app_file file.

Also, it displays messages for each installation step.

Let’s make the above script executable:
```bash
chmod +x install_from_file.sh
```
Then, we run the script with the name of the text file as an argument. This installs the packages listed in the text file:
```bash
./install_from_file.sh app_list.txt
```
Particularly, this method keeps a consistent list of application installations over multiple systems. However, it requires us to create and maintain a plain text file.




Apps I install

