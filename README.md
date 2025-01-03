  🚀 **Born2beroot**  

## Table of Contents  
1. **Introduction**  
   - What is a Virtual Machine?  
   - How do Virtual Machines Work?  
   - What is LVM?  
   - What is AppArmor?  
   - Apt vs. Aptitude  
   - Using SSH  
   - Implementing UFW with SSH  
   - cron and wall  

2. **Installation**  
   - **sudo**  
     - Step 1: Installing sudo  
     - Step 2: Adding User to sudo Group  
     - Step 3: Running root-Privileged Commands  
     - Step 4: Configuring sudo  

3. **SSH Setup**  
   - Step 1: Installing & Configuring SSH  
   - Step 2: Installing & Configuring UFW  
   - Step 3: Connecting to the Server via SSH  

4. **User Management**  
   - Step 1: Setting a Strong Password Policy  
     - Password Age  
     - Password Strength  
   - Step 2: Creating a New User  
   - Step 3: Creating a New Group  

5. **Automating with cron**  
   - Setting Up a cron Job  

6. **Monitoring**  

7. **Bonus Section**  
   - **LLMP Stack Installation**  
     - Step 1: Installing Lighttpd  
     - Step 2: Installing & Configuring MariaDB  
     - Step 3: Installing PHP  
     - Step 4: Downloading & Configuring WordPress  
     - Step 5: Configuring Lighttpd  
   - **FTP**  
     - Step 1: Installing & Configuring FTP  
     - Step 2: Connecting to Server via FTP  

8. **Submission & Peer Evaluation**  
   - For 1337/42 Students  
-----

## Introduction  
In this project, you'll create your first machine in VirtualBox (or UTM if VirtualBox is unavailable) following specific instructions. By the end, you'll be able to set up your own operating system while implementing strict guidelines.

## What is a Virtual Machine?  
A Virtual Machine (VM) is a software environment that enables the installation of an operating system within itself, making it appear as if it is running on a physical computer. Virtual machines simulate physical devices such as CPU, memory, network interface, and storage, all powered by the host machine. The hypervisor is responsible for creating and managing VMs by isolating VM resources from the host system.

### Key Concepts:  
- **Host Machine**: The physical device that provides hardware resources for the VM.  
- **Guest Machine**: The virtualized environment running on the host machine.  
- **Hypervisor**: The software managing and isolating VMs from system hardware.

Benefits include running multiple OSs on a single machine, testing unstable programs safely, efficient resource sharing, cost reduction, and easy VM cloning across devices.

## How do Virtual Machines Work?  
Virtualization enables the sharing of a system's resources among multiple virtual environments. The hypervisor manages resource allocation between the host and guest machines. If a guest requires more resources, the hypervisor ensures the request is handled efficiently.

### Advantages:  
- Run multiple OSs simultaneously on the same machine.  
- Safe environment for testing unstable programs.  
- Improved use of shared resources.  
- Reduced physical infrastructure costs.  
- Easy implementation and cloning of VMs.

## What is LVM?  
LVM (Logical Volume Manager) is an abstraction layer between storage devices and file systems, providing greater flexibility for partition management. LVM allows partition resizing, expansion, and movement across physical disks without worrying about contiguous space.

### Key Concepts:  
- **Physical Volume (PV)**: The actual storage device.  
- **Volume Group (VG)**: A virtual storage pool built from PVs.  
- **Logical Volume (LV)**: The partitions created within VGs, used for file systems, swaps, or VMs.

## What is AppArmor?  
AppArmor is a security tool that uses Mandatory Access Control (MAC) to restrict what actions processes can perform. For instance, if an application tries to access the camera and the administrator denies this, AppArmor prevents it from doing so.

### Modes:  
- **Enforce Mode**: Prevents restricted actions.  
- **Complain Mode**: Logs restricted actions without blocking them.

## Difference Between Apt and Aptitude  
APT (Advanced Package Tool) and Aptitude are both used for managing packages on Debian-based distributions. APT simplifies package installation and dependency management via command-line tools like `apt-get` and `apt-cache`. Aptitude, a graphical interface, offers better dependency control and allows users to choose between various dependencies.

## How to Use SSH?  
SSH (Secure Shell) enables secure remote administration of servers over the Internet. It uses encryption techniques to ensure that communication between the client and host is secure. 

### SSH Encryption Methods:  
- **Symmetric Encryption**: Uses the same key for encryption and decryption.  
- **Asymmetric Encryption**: Uses a public-private key pair.  
- **Hashing**: Provides integrity without decryption.

To connect, use the following command:  
`ssh {username}@{IP_host} -p {port}`

## How to Implement UFW with SSH  
UFW (Uncomplicated Firewall) simplifies firewall management by offering an interface for configuring iptables. Once installed, UFW can be used to control which ports are open or closed, enhancing security, especially when combined with SSH.

## What is cron and What is wall?  
- **Cron**: A Linux task manager that automates command execution at specified times. For example, scheduling a server restart daily at 4:00 AM.  
- **Wall**: A command used by the root user to broadcast messages to all users logged into the system, useful for notifying of important system changes.

---

```bash
# Install and Configure sudo
sudo apt install sudo
sudo usermod -aG sudo <username>
sudo -v

# Install and Configure SSH
sudo apt install openssh-server
# Edit /etc/ssh/sshd_config to set Port 4242 and PermitRootLogin no
sudo systemctl status ssh

# Configure UFW (Firewall)
sudo apt install ufw
sudo ufw enable
sudo ufw allow 4242

# User and Password Management
# Edit /etc/login.defs to set password expiration
sudo apt install libpam-pwquality
# Edit /etc/pam.d/common-password for password policies

# Create Users and Groups
sudo adduser <username>
sudo addgroup <groupname>
sudo adduser <username> <groupname>

# Configure Cron Job
sudo crontab -u root -e
# Example cron job every 10 minutes:
*/10 * * * * sh /path/to/script

# Create Monitoring Script (monitoring.sh)
#!/bin/bash
echo "OS and Kernel: $(uname -a)"
echo "CPU Info: $(lscpu)"
echo "RAM Usage: $(free -h)"
echo "Last Reboot: $(who -b)"
# Schedule cron job
sudo crontab -u root -e
```
----

# Install Lighttpd
sudo apt install lighttpd
sudo ufw allow 80

# Install MariaDB
sudo apt install mariadb-server
sudo mysql_secure_installation
CREATE DATABASE <db-name>;
GRANT ALL ON <db-name>.* TO '<user>'@'localhost' IDENTIFIED BY '<password>';
FLUSH PRIVILEGES;

# Install PHP
sudo apt install php-cgi php-mysql

# Install WordPress
sudo apt install wget
sudo wget http://wordpress.org/latest.tar.gz -P /var/www/html
sudo tar -xzvf /var/www/html/latest.tar.gz -C /var/www/html
sudo rm /var/www/html/latest.tar.gz
sudo cp /var/www/html/wordpress/* /var/www/html/
sudo rm -rf /var/www/html/wordpress
sudo cp /var/www/html/wp-config-sample.php /var/www/html/wp-config.php

# Configure Lighttpd for PHP
sudo lighty-enable-mod fastcgi fastcgi-php
sudo service lighttpd force-reload

# Install FTP (vsftpd)
sudo apt install vsftpd
sudo ufw allow 21
sudo vi /etc/vsftpd.conf
# Enable write access and set FTP root
sudo mkdir /home/<user>/ftp
sudo chmod a-w /home/<user>/ftp
user_sub_token=$USER
local_root=/home/$USER/ftp
echo <user> | sudo tee -a /etc/vsftpd.userlist

# Connect via FTP
ftp <ip-address>
----

### Submission & Peer-Evaluation Guide for 1337/42 Students

1. **Creating the Signature File**:
   - At the root of your Git repository, create a `signature.txt` file.
   - Include the virtual machine disk signature in sha1 format (e.g., from a `.vdi` or `.qcow2` file). Use the following steps depending on your OS:

   **Windows**:
   - Navigate to: `%HOMEDRIVE%%HOMEPATH%\VirtualBox VMs\`
   - Execute the command: `certUtil -hashfile centos_serv.vdi sha1`

   **Linux**:
   - Navigate to: `~/VirtualBox VMs/`
   - Execute the command: `sha1sum centos_serv.vdi`

   **Mac M1**:
   - Navigate to: `~/Library/Containers/com.utmapp.UTM/Data/Documents/`
   - Execute the command: `shasum Centos.utm/Images/disk-0.qcow2`

   **MacOS**:
   - Navigate to: `~/VirtualBox VMs/`
   - Execute the command: `shasum centos_serv.vdi`

2. **Evalknowledge.txt**:
   - Includes a Q&A section with things to check as an evaluator.

3. **Recommendation**:
   - For better retention, repeat the installation steps multiple times, particularly if it's your first experience with Linux and virtual machines.

