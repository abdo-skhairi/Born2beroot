![Alt text](https://raw.githubusercontent.com/abdo-skhairi/Born2beroot/refs/heads/main/preview.webp)

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

## Introduction  📘
In this project, you'll create your first machine in VirtualBox (or UTM if VirtualBox is unavailable) following specific instructions. By the end, you'll be able to set up your own operating system while implementing strict guidelines.

## What is a Virtual Machine?  🖥️
A Virtual Machine (VM) is a software environment that enables the installation of an operating system within itself, making it appear as if it is running on a physical computer. Virtual machines simulate physical devices such as CPU, memory, network interface, and storage, all powered by the host machine. The hypervisor is responsible for creating and managing VMs by isolating VM resources from the host system.

### Key Concepts:  
- **Host Machine**: The physical device that provides hardware resources for the VM.  🏠💻
- **Guest Machine**: The virtualized environment running on the host machine.  🎛️🖥️
- **Hypervisor**: The software managing and isolating VMs from system hardware. 🖧

Benefits include running multiple OSs on a single machine, testing unstable programs safely, efficient resource sharing, cost reduction, and easy VM cloning across devices.
-----

## How do Virtual Machines Work?  🖥️
Virtualization enables the sharing of a system's resources among multiple virtual environments. The hypervisor manages resource allocation between the host and guest machines. If a guest requires more resources, the hypervisor ensures the request is handled efficiently.

### Advantages:  
- Run multiple OSs simultaneously on the same machine.  
- Safe environment for testing unstable programs.  
- Improved use of shared resources.  
- Reduced physical infrastructure costs.  
- Easy implementation and cloning of VMs.

## What is LVM?  📦🔧
LVM (Logical Volume Manager) is an abstraction layer between storage devices and file systems, providing greater flexibility for partition management. LVM allows partition resizing, expansion, and movement across physical disks without worrying about contiguous space.

### Key Concepts:  
- **Physical Volume (PV)**: The actual storage device.  
- **Volume Group (VG)**: A virtual storage pool built from PVs.  
- **Logical Volume (LV)**: The partitions created within VGs, used for file systems, swaps, or VMs.

## What is AppArmor?  🛡️📜
AppArmor is a security tool that uses Mandatory Access Control (MAC) to restrict what actions processes can perform. For instance, if an application tries to access the camera and the administrator denies this, AppArmor prevents it from doing so.

### Modes:  
- **Enforce Mode**: Prevents restricted actions.  
- **Complain Mode**: Logs restricted actions without blocking them.

## Difference Between Apt and Aptitude  🔍
APT (Advanced Package Tool) and Aptitude are both used for managing packages on Debian-based distributions. APT simplifies package installation and dependency management via command-line tools like `apt-get` and `apt-cache`. Aptitude, a graphical interface, offers better dependency control and allows users to choose between various dependencies.

## How to Use SSH?  🔒
SSH (Secure Shell) enables secure remote administration of servers over the Internet. It uses encryption techniques to ensure that communication between the client and host is secure. 

### SSH Encryption Methods:  
- **Symmetric Encryption**: Uses the same key for encryption and decryption.  
- **Asymmetric Encryption**: Uses a public-private key pair.  
- **Hashing**: Provides integrity without decryption.

To connect, use the following command:  
`ssh {username}@{IP_host} -p {port}`

## How to Implement UFW 🛡️ with SSH 🔒
UFW (Uncomplicated Firewall) simplifies firewall management by offering an interface for configuring iptables. Once installed, UFW can be used to control which ports are open or closed, enhancing security, especially when combined with SSH.

## What is cron and What is wall?  ⏰🗓️
- **Cron**: A Linux task manager that automates command execution at specified times. For example, scheduling a server restart daily at 4:00 AM.  
- **Wall**: A command used by the root user to broadcast messages to all users logged into the system, useful for notifying of important system changes.

---

# **System Configuration Commands**

## 🧑‍💻 **Install and Configure `sudo`**  
```bash
# Install sudo package
sudo apt install sudo

# Add a user to the sudo group
sudo usermod -aG sudo <username>

# Verify sudo access
sudo -v
```

---

## 🔐 **Install and Configure SSH**  
```bash
# Install the SSH server
sudo apt install openssh-server

# Edit configuration to enhance security
# Open /etc/ssh/sshd_config and set:
# - Port 4242
# - PermitRootLogin no

# Check the SSH service status
sudo systemctl status ssh
```

---

## 🛡️ **Configure UFW (Firewall)**  
```bash
# Install UFW
sudo apt install ufw

# Enable the firewall
sudo ufw enable

# Allow custom SSH port
sudo ufw allow 4242
```

---

## 🔒 **User and Password Management**  
```bash
# Set password expiration policies
# Edit /etc/login.defs

# Install the PAM quality module for password strength
sudo apt install libpam-pwquality

# Configure password policies in /etc/pam.d/common-password
```

---

## 👥 **Create Users and Groups**  
```bash
# Add a new user
sudo adduser <username>

# Create a new group
sudo addgroup <groupname>

# Add a user to a group
sudo adduser <username> <groupname>
```

---

## ⏰ **Configure Cron Jobs**  
```bash
# Edit root's crontab file
sudo crontab -u root -e

# Example: Run a script every 10 minutes
*/10 * * * * sh /path/to/script
```

8.7 - Configuring Sudoers file, logs, warning message
cd /var/log : Access the location where log files are stored, providing information about system events, services, processes.

Each action using sudo has to be archived, both inputs and outputs. To do so, create a folder (name it sudo for clarity), then create a file.log, and save the path to that file.

sudo vim /etc/sudoers or sudo visudo : Access the sudoers file responsible for defining the rules and permissions that determine which users or groups are allowed to execute commands with elevated privileges using the sudo command.

Defaults	badpass_message="Wrong password, please try again!" : Adding warning message ****

Defaults passwd_tries=3 : Sets a default value for the maximum number of password entry attempts allowed when a user runs sudo.

Defaults	logfile="/var/log/sudo/sudo.log" : Sets the location for the sudo log file.

Defaults	log_input, log_output : Enable logging of both input (commands typed by user) and output (result) for sudo commands.

Defaults	requiretty : (teletypewriter) By requiring a TTY, it limits the ability of users to run sudo commands from scripts or automated processes by adding an extra layer of authentication ensuring that users physically present at the console are the ones executing privileged commands.



---

## 📊 **Create a Monitoring Script**  
```bash
#!/bin/bash
arc=$(uname -a)
pcpu=$(grep "physical id" /proc/cpuinfo | sort | uniq | wc -l)
vcpu=$(grep "^processor" /proc/cpuinfo | wc -l)
fram=$(free -m | awk '$1 == "Mem:" {print $2}')
uram=$(free -m | awk '$1 == "Mem:" {print $3}')
pram=$(free | awk '$1 == "Mem:" {printf("%.2f"), $3/$2*100}')
fdisk=$(df -Bg | grep '^/dev/' | grep -v '/boot$' | awk '{ft += $2} END {print ft}')
udisk=$(df -Bm | grep '^/dev/' | grep -v '/boot$' | awk '{ut += $3} END {print ut}')
pdisk=$(df -Bm | grep '^/dev/' | grep -v '/boot$' | awk '{ut += $3} {ft+= $2} END {printf("%d"), ut/ft*100}')
cpul=$(top -bn1 | grep '^%Cpu' | cut -c 9- | xargs | awk '{printf("%.1f%%"), $1 + $3}')
lb=$(who -b | awk '$1 == "system" {print $3 " " $4}')
lvmt=$(lsblk | grep "lvm" | wc -l)
lvmu=$(if [ $lvmt -eq 0 ]; then echo no; else echo yes; fi)
#You need to install net tools for the next step [$ sudo apt install net-tools]
ctcp=$(cat /proc/net/sockstat{,6} | awk '$1 == "TCP:" {print $3}')
ulog=$(users | wc -w)
ip=$(hostname -I)
mac=$(ip link show | awk '$1 == "link/ether" {print $2}')
cmds=$(journalctl _COMM=sudo | grep COMMAND | wc -l) # journalctl should be running as sudo but our script is running as root so we don't need in sudo here
wall "	#Architecture: $arc
	#CPU physical: $pcpu
	#vCPU: $vcpu
	#Memory Usage: $uram/${fram}MB ($pram%)
	#Disk Usage: $udisk/${fdisk}Gb ($pdisk%)
	#CPU load: $cpul
	#Last boot: $lb
	#LVM use: $lvmu
	#Connexions TCP: $ctcp ESTABLISHED
	#User log: $ulog
	#Network: IP $ip ($mac)
	#Sudo: $cmds cmd" # broadcast our system information on all terminals

```

---

### 🕒 **Schedule the Monitoring Script with Cron**  
```bash
# Schedule the monitoring script
sudo crontab -u root -e

# Add an entry to execute the script periodically
*/10 * * * * /path/to/monitoring.sh
```
---

# ⚙️ **Server Setup Commands**

## 🌐 **Install and Configure Lighttpd**  
```bash
# Install Lighttpd
sudo apt install lighttpd

# Allow HTTP traffic through the firewall
sudo ufw allow 80
```

---

## 🛢️ **Install and Configure MariaDB**  
```bash
# Install MariaDB server
sudo apt install mariadb-server

# Secure the installation
sudo mysql_secure_installation

# Create a new database
CREATE DATABASE <db-name>;

# Grant privileges to a user
GRANT ALL ON <db-name>.* TO '<user>'@'localhost' IDENTIFIED BY '<password>';

# Apply changes
FLUSH PRIVILEGES;
```

---

## 💻 **Install PHP**  
```bash
# Install PHP modules for CGI and MariaDB integration
sudo apt install php-cgi php-mysql
```

---

## 📝 **Install and Configure WordPress**  
```bash
# Install wget if not already installed
sudo apt install wget

# Download WordPress
sudo wget http://wordpress.org/latest.tar.gz -P /var/www/html

# Extract the WordPress archive
sudo tar -xzvf /var/www/html/latest.tar.gz -C /var/www/html

# Remove the downloaded archive
sudo rm /var/www/html/latest.tar.gz

# Move WordPress files to the web root
sudo cp /var/www/html/wordpress/* /var/www/html/

# Remove leftover WordPress directory
sudo rm -rf /var/www/html/wordpress

# Create the configuration file
sudo cp /var/www/html/wp-config-sample.php /var/www/html/wp-config.php
```

---

## 🛠️ **Configure Lighttpd for PHP**  
```bash
# Enable FastCGI and PHP modules for Lighttpd
sudo lighty-enable-mod fastcgi fastcgi-php

# Reload Lighttpd to apply changes
sudo service lighttpd force-reload
```

---

## 📡 **Install and Configure FTP (vsftpd)**  
```bash
# Install the FTP server
sudo apt install vsftpd

# Allow FTP traffic through the firewall
sudo ufw allow 21

# Open the vsftpd configuration file
sudo vi /etc/vsftpd.conf

# Enable write access and set FTP root directory
sudo mkdir /home/<user>/ftp
sudo chmod a-w /home/<user>/ftp
user_sub_token=$USER
local_root=/home/$USER/ftp

# Add the user to the vsftpd user list
echo <user> | sudo tee -a /etc/vsftpd.userlist
```
---

### **Peer-Evaluation Guide for 1337/42 Students** 👥

#### **1. Submission** 📥
- Submit a `signature.txt` file at the root of your Git repository.
- Include the virtual disk signature (sha1 hash) of your machine.

#### **2. How to Get the Signature** 🔑
- **Windows**: `%HOMEDRIVE%%HOMEPATH%\VirtualBox VMs\`
  - Command: `certUtil -hashfile centos_serv.vdi sha1`
  
- **Linux**: `~/VirtualBox VMs/`
  - Command: `sha1sum centos_serv.vdi`
  
- **Mac M1**: `~/Library/Containers/com.utmapp.UTM/Data/Documents/`
  - Command: `shasum Centos.utm/Images/disk-0.qcow2`
  
- **MacOS**: `~/VirtualBox VMs/`
  - Command: `shasum centos_serv.vdi`

#### **3. Example Output** 💻
- **Output Format**: `6e657c4619944be17df3c31faa030c25e43e40af`

#### **4. Evalknowledge.txt** 📄
- Includes Q&A from the subject and evaluation checklist.
  
#### **5. Additional Tips** 📝💡
- Repeat the installation process several times to reinforce your understanding, especially if this is your first experience with both Linux and virtualization.

