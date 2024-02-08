# Bar-Ilan University DevSecOps

## Table of Contents
- [Linux Administration - Lesson 2 - 19.12.2023](#lesson-2---19122023)
  - [Basic Commands](#basic-commands)
- [Linux Administration - Lesson 3 - 02.01.2024](#lesson-3---02012024)
  - [Find and Grep](#work-with-find--grep)
  - [Disk and Partitions](#disk-and-partitions)
- [Linux Administration - Lesson 4 - 05.01.2024](#lesson-4---05012024)
  - [User Management](#user-management)
- [Linux Administration - Lesson 6 - 12.01.2024](#lesson-6---12012024)
  - [Package Management](#package-management)
  - [General Services](#general-services)
- [Linux Administration - Lesson 7 - 16.01.2024](#lesson-7---16012024)
  - [Network Management](#network-management)
- [Linux Administration - Lesson 8 - 19.01.2024](#lesson-8---19012024)
  - [Containers](#containers)
- [Git - Lesson 9 - 23.01.2024](#lesson-9---23012024)
  - [Git Commands](#git-commands)
- [Git - Lesson 10 - 26.01.2024](#lesson-10---26012024)
  - [GitHub Commands](#github-commands)
- [Git - Lesson 11 - 30.01.2024](#lesson-11---30012024)
  - [GitHub Commands](#github-commands)
  - [BASH](#bash)

## Lesson 2 - 19.12.2023

### Basic Commands
- `sudo` - Run the subsequent command with superuser privileges
- `pwd` - Print the current working directory
- `cd` - Change to the user's home directory
- `mkdir` - Create a new directory (replace 'new_directory' with the desired directory name)
- `ls -a` - List all files, including hidden ones, in the current directory
- `ls -il <path>` - Display detailed information about files in the specified path, including inode numbers
- `apt update` - Update the package list to get information on the newest versions of packages
- `apt upgrade` - Upgrade installed packages to their latest versions
- `cp` - Copy files or directories
- `mv` - Move or rename files or directories
- `rm` - Remove files or directories (use with caution)
- `nano` - Open the Nano text editor (replace with your preferred text editor)
- `cat` - Display the content of a file
- `man` - Display the manual page for a command
- `chmod` - Change file permissions
- `chown` - Change file ownership
- `ps` - Display a snapshot of the currently running processes
- `top` - Display a dynamic view of system processes
- `kill` - Terminate a process by sending a signal
- `grep` - Search for a pattern in files
- `df` - Display disk space usage
- `du` - Display file and directory space usage
- `history` - Display command history
- `ifconfig` - Display network interface configuration

## Lesson 3 - 02.01.2024

### Work with find / grep
- `find / -type f -links +1 -exec ls -i {} +` - Find all hard links in "/" Directory
- `find /path/to/search -type f -exec grep -l 'search_text' {} +` - List files with specified text
- `find /path/to/search -type f -mtime -N -exec ls -l {} \;` - List files modified in the last N days
- `find /path/to/search -type f -name 'pattern*' -exec rm {} \;` - Delete files matching a pattern
- `find /path/to/search -type f -name '*.txt'` - List all .txt files
- `find /path/to/search -type f -name '*.txt' -exec wc -l {} +` - Count lines in all .txt files
- `search_dir="/path/to/search"` - Define the directory to search
- `find "$search_dir" -name "filename.txt"` - Find files by name
- `find "$search_dir" -name "*.log"` - Find files by extension
- `find "$search_dir" -type f` - Find and list files in a directory
- `find "$search_dir" -type d` - Find and list directories
- `grep -E "$(tail -2 /etc/passwd | sort -r | grep '/home' | cut -d: -f1 | paste -sd '|')" /var/log/auth.log` - Find 2 last created users and search for authentication

### Disk and Partitions
- `lsblk` - List Block Devices
- `sudo cfdisk /dev/sd*` - Create partition (cfdisk or fdisk)
- `sudo mkfs -t ext4 /dev/sdb**` - Create file system
- `sudo mkdir /new_directory` - Create directory for partition
- `sudo mount /dev/sdb* /new_directory` - Mount new partition to directory
- `sudo nano /etc/fstab` - Edit file system table
- `/dev/sdb*  /new_directory  ext4  defaults  0  0` - Add a line to fstab so it will be applied after reboot
- `sudo resize2fs /dev/sdb*` - Resize partition
- `sudo dd if=/source of=/destination` - Copy data from 'source' to 'destination'

## Lesson 4 - 05.01.2024

### User Management
- `cat /etc/passwd` - username:password:userID:groupID:comment:homeDirectory:shell
- `cat /etc/login.defs` - Displaying configuration settings for user authentication and password policies
- `sudo adduser username` - Creating a new user; replace 'username' with the desired username
- `sudo adduser -m -d /home/username -G sudo -s /bin/bash username` - Create a user with a home dir added to the sudoers group
- `passwd username` - Changing user password; replace 'username' with the target username
- `cat /etc/group` - Add users to group
- `id username` - Viewing user information; replace 'username' with the target username
- `sudo chsh -s /bin/bash username` - Changing the user's default shell; replace 'username' with the target username
- `sudo usermod -aG groupname username` - Adding a user to a group; replace 'username' and 'groupname' accordingly
- `usermod -a -G wheel USERNAME` - Add a user to the wheel group in RHEL (sudo)
- `sudo chown :groupname filename` - Changing group ownership of a file; replace 'groupname' and 'filename' accordingly
- `sudo chown username:filename` - Changing user ownership of a file; replace 'username' and 'filename' accordingly
- `sudo deluser username` - Deleting a user; replace 'username' with the username to be deleted
- `sudo deluser username groupname` - Removing a user from a group; replace 'username' and 'groupname' accordingly

## Lesson 6 - 12.01.2024

### Package Management 
- `rpm -qa` - List all installed packages
- `rpm -qi packageName` - Query information about a specific package. Replace "packageName" with the name of the package
- `rpm -ivh /path/to/package.rpm` - Install a package from an RPM file. Replace "/path/to/package.rpm" with the actual path to the RPM file
- `rpm -Uvh /path/to/new_package.rpm` - Upgrade an installed package. Replace "/path/to/new_package.rpm" with the path to the new version of the RPM file
- `rpm -e packageName` - Remove an installed package. Replace "packageName" with the name of the package you want to uninstall
- `cat /etc/yum.repos.d/redhat.repo` - Package Repositories
- `apt list` - List packages based on package names
- `apt search` - Search in package descriptions
- `apt show` - Show package details
- `apt install` - Install packages
- `apt reinstall` - Reinstall packages
- `apt remove` - Remove packages
- `apt autoremove` - Remove automatically all unused packages
- `apt update` - Update list of available packages
- `apt upgrade` - Upgrade the system by installing/upgrading packages
- `apt full-upgrade` - Upgrade the system by removing/installing/upgrading packages
- `apt edit-sources` - Edit the source information file
- `apt satisfy` - Satisfy dependency strings

### General Services
- `systemctl status ServiceName` - Get Service Status
- `systemctl start ServiceName` - Start Service Status
- `systemctl stop ServiceName` - Stop Service Status
- `systemctl restart ServiceName` - Restart Service Status
- `systemctl enable ServiceName` - Start Service Status on Boot
- `systemctl cat ServiceName` - This command will output the complete content of the service unit file

## Lesson 7 - 16.01.2024

### Network Management
- `sudo apt-get install network-manager` - Install Network Manager
- `nmcli` - CLI Commands
- `nmtui` - GUI Interface
- `nmcli connection show` - Show all network connections
- `nmcli device wifi list` - Display available Wi-Fi networks
- `nmcli device show | grep IP4.DNS` - Show DNS Configuration
- `sudo nano /etc/hostname` - Change Host name
- `sudo nano /etc/hosts` - Local HOST DNSs
- `sudo nano /etc/resolv.conf` - Configure DNS on ALL Interfaces (Not Recommended)
- `sudo traceroute IP` - Trace route
- `nc -l 2000` - Netcat listen to port 2000
- `nc IP 2000` - Connect using netcat to IP on port 2000
- `curl https://google.com:443` - Sends a simple HTTP GET request to the server on the specified port
- `cd /etc/netplan/` - Edit Netplan to change IP Address
  ```yaml
  # This file describes the network interfaces available on your system
  # For more information, see netplan(5).
  network:
    version: 2
    renderer: networkd
    ethernets:
      enp0s3:
       dhcp4: no
       addresses: [192.168.1.222/24]
       gateway4: 192.168.1.1
       nameservers:
         addresses: [8.8.8.8, 8.8.4.4]
 - -sudo netplan apply-


  

## Lesson 8 - 19.01.2024

### Containers
- `docker login` - Login to DockerHub
- `docker pull IMAGE` - Pull image from Repository
- `docker tag myapp yourdockerhubaccount/myapp:v1.0` - Tagging a Docker image with a new name and optional tag
- `docker push account/image_name:tag ` - Push Image to DockerHub
- `docker search IMAGE` - Search image in the repository
- `docker build -t TAG .` - Build an image from Dockerfile
- `docker run -p 8080:80 --name MY_IMAGE_NAME IMAGE_ID` - Run container with our name
- `docker run -it IMAGE_ID /bin/bash` - Run a container from an image with a terminal with bash commands
- `docker run -d -p 8080:80 IMAGE_ID` - Run a container in Daemon(Service) mode and publish port 8080 to 80
- `docker ps` - Show all active containers
- `docker ps -a` - Show all containers
- `docker images` - Show all local Images
- `docker rmi Contained_ID -f` - Force remove running Container
- `ARG DEBIAN_FRONTEND=noninteractive` - Skip promts (Add to Dockerfile as step)

## Lesson 9 - 23.01.2024

### Git Commands
- `git init` - Initialize a new Git repository in the current directory
- `git config user.name <Username>` - Configure user name for Git ONLY for current repository
- `git config user.email <Email>` - Configure email for Git ONLY for current repository
- `git config --global user.name <Username>` - Configure user name for Git Globally
- `git config --global user.email <email>` - Configure email for Git Globally
- `git status` - Display the status of the working directory and staging area
- `git add .` - Add changes in the working directory to the staging area to all files
- `git add <file>` - Add changes in the working directory to the staging area to specific files
- `git rm --cached <file>` - Remove a file from the staging area while keeping it in the working directory
- `git commit -m "Initial Commit"` - Commit the staged changes with a descriptive message
- `git commit` - Commit the staged change using Text Editor
- `git restore <file>` - Discard changes in the working directory and restore the specified file to its last committed state
- `git checkout <file>` ` Discard changes in the working directory and restore the specified file to its last committed state
- `git log` - Display a log of commits, showing commit hashes, authors, dates, and commit messages
- `git branch <NewBranchName>` - Create a new branch with the specified name
- `git branch` Display a list of existing branches and highlight the current branch
- `git merge <source_branch>` - Merge changes from another branch into the current branch

## Lesson 10 - 26.01.2024

### GitHub Commands
- `ssh-keygen` - Generate a new SSH key pair (Copy PUBLIC Key to GitHub)
- `eval "$(ssh-agent -s)"` - Start the SSH agent in Linux
- `start-ssh-agent` - Start SSH Agent in Windows
- `ssh-add <KeyName>` - Add the SSH private key to the SSH agent 
- `git log --graph` - Show commit history with a graphical representation of branches and merges
- `git clone <repo>` - Clone a repository
- `git remote add <origin> <git@github.com:username/repo.git>` - Add a remote named "origin" pointing to the repository
- `git push --set-upstream origin main` - Push local changes to the remote repository named "origin" and Set up the tracking relationship for the "main" branch


## Lesson 11 - 30.01.2024

### GitHub Commands
- `git remote -v` - Display URLs for remote repositories (fetch and push)
- `git branch -a` - List all branches (local and remote-tracking)
- `git branch -r` - List only remote-tracking branches
- `git fetch` - Fetch the latest changes from the remote repository (no automatic merge)
- `git checkout -b <RemoteBranch> remotes/origin/<SecondBranch>` - Create a new local branch and set up tracking from a remote branch
- `git branch -d <BranchToDelete>` - Delete the local branch '<BranchToDelete>'

## Lesson 12 - 02.02.2024

### BASH Basics

# BASH Scripting Examples

## Hello World Script:

```bash
#!/bin/bash
# This is a simple Hello World script in BASH

echo "Hello, World!"
```

##  User Input Script:
```bash
#!/bin/bash
# A script that takes user input and displays a message

echo "Enter your name:"
read name

echo "Hello, $name! Welcome to the world of BASH scripting."
```
## File Manipulation Script:
```bash
#!/bin/bash
# A script to manipulate files

# Create a new directory
mkdir my_files

# Navigate to the new directory
cd my_files

# Create three empty files
touch file1.txt
touch file2.txt
touch file3.txt

# Display the list of files in the directory
echo "Files in the directory:"
ls
```












