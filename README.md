# 🛡️Virtual Lab Setup on VMware Workstation (Windows 11 Host)

## 📖 Project Overview
This repository documents the step-by-step process I followed to set up a **personal cybersecurity lab** using **Kali Linux** as a virtual machine on my **Windows 11 system** with **VMware Workstation Player**.

The primary goal of this lab is to build a controlled environment for practicing:
- **Penetration Testing**
- **Web Application Exploitation**
- **SOC Analysis**
- **GRC Projects**

---

## 🖥️ Host Machine Specifications

| Specification | Details |
|---------------|---------|
| **Operating System** | Windows 11 |
| **RAM** | Minimum 8 GB |
| **Processor** | Intel i5 / AMD Ryzen equivalent |
| **Storage** | At least 50 GB free space |

---

## 📥 Tools and Resources Used

| Tool | Source | Notes |
|------|--------|-------|
| **Kali Linux ISO** | [kali.org](https://www.kali.org/get-kali/) | Latest stable release |
| **VMware Workstation Player** | [TechSpot Download Link](https://www.techspot.com/downloads/downloadnow/189/?evp=f14a48a23bc560f5fbe81b8d83387b41&file=11957) | Free version |
| **Windows 7 ISO** | Microsoft (Archived) / Trusted Source | Target machine |
| **Metasploitable 2** | [SourceForge](https://sourceforge.net/projects/metasploitable/) | Vulnerable Linux VM |
| **DVWA** | [GitHub Repo](https://github.com/digininja/DVWA) | Web app for testing |

---

## 🛠️ Step-by-Step Walkthrough

### ✅ 1. Install and Configure Kali Linux VM

#### 📥 Download Kali Linux ISO
   Go to [kali.org/get-kali](https://www.kali.org/get-kali/) and download the latest ISO.

#### 💿 Install VMware Workstation Player
   Install using default installation options.

#### 🖥️ Create a New VM
   - Select *Typical (Recommended)*.
   - Choose Kali ISO.
   - Allocate:
     - CPU: 1 Core  
     - RAM: 2 GB  
     - Disk: 20 GB (Dynamic)  
     - Network: NAT  

#### 💿 Install Kali Linux
   Follow installer prompts → Default partitioning → Create user.

**First Boot & Updates**
   bash
   sudo apt update && sudo apt upgrade -y

---
   
### 🎯 2. Add Target Machine – Windows 7 VM

#### 📥 Download Windows 7 ISO
Use an official or archived Microsoft ISO.

#### 🖥️ Create New VM in VMware
- Select **Typical (Recommended)** → Choose ISO → Name VM `Windows7-Target`.
- Allocate:
  - **CPU:** 1 Core  
  - **RAM:** 2 GB  
  - **Disk:** 40 GB  
- Choose **NAT** or **Host-Only Network** to keep it isolated.

#### 💿 Install Windows 7
- Follow installation wizard (default setup).
- Disable Windows Defender/Firewall for ease of exploitation.
- Create a **low-privilege test user account**.

#### 📸 Take a Snapshot
Take a VM snapshot after installation so you can restore easily later.

---

### 🎯 3. Add Target Machine – Metasploitable 2 VM

#### 📥 Download Metasploitable 2 VM
Download from [SourceForge](https://sourceforge.net/projects/metasploitable/).

#### 🖥️ Import into VMware
- Extract the downloaded ZIP.  
- Open the `.vmx` file in VMware.

#### 🌐 Configure Network
Set network to **Host-Only** (recommended for safety).

#### ▶️ Start VM
Default credentials:
bash
username: msfadmin
password: msfadmin

---

🌐 DVWA Setup on Kali Linux – Home Lab

This repository documents the **complete process of setting up Damn Vulnerable Web Application (DVWA)** on **Kali Linux** as part of my **Home Cybersecurity Lab**.  

DVWA is an intentionally vulnerable PHP/MySQL web application designed for practicing **web application penetration testing** techniques in a safe, isolated environment.



## 🖥️ Lab Overview

| Component           | Details |
|--------------------|---------|
| **Host OS**        | Windows 11 |
| **Virtualization** | VMware Workstation Player |
| **Attacker VM**    | Kali Linux (Latest ISO) |
| **Target VM**      | DVWA (Hosted on Kali) |
| **Network Mode**   | Host-Only (Isolated) |

> 🛡 **Safety Note:** Host-Only network mode ensures your vulnerable setup is isolated from the internet and cannot affect your main network.

---

## 📦 Step 1: Install Required Packages

Run the following commands in Kali Linux terminal:

bash
sudo apt update
sudo apt install apache2 mariadb-server php php-mysqli php-gd libapache2-mod-php -y
This installs:

Apache2 → Web server

MariaDB → Database server

PHP & Modules → For running DVWA

---

▶️ Step 2: Start and Enable Services
Enable and start Apache and MariaDB:

bash
Copy code
sudo systemctl start apache2
sudo systemctl enable apache2
sudo systemctl start mariadb
sudo systemctl enable mariadb

✅ Enabling ensures these services start automatically on VM boot.

---

📥 Step 3: Clone DVWA
Navigate to the web root and clone DVWA:

bash
Copy code
cd /var/www/html
sudo git clone https://github.com/digininja/DVWA.git
sudo chown -R www-data:www-data DVWA

---

🗄️ Step 4: Configure the Database
Enter MySQL shell:

bash
Copy code
sudo mysql -u root
Inside MySQL, run:

sql
Copy code
CREATE DATABASE dvwa;
CREATE USER 'dvwa'@'localhost' IDENTIFIED BY 'dvwa';
GRANT ALL PRIVILEGES ON dvwa.* TO 'dvwa'@'localhost';
FLUSH PRIVILEGES;
EXIT;

---

⚙️ Step 5: Configure DVWA
Copy and edit DVWA configuration file:

bash
Copy code
cd /var/www/html/DVWA/config
sudo cp config.inc.php.dist config.inc.php
sudo nano config.inc.php
Update database credentials inside config.inc.php:

php
Copy code
$_DVWA['db_user'] = 'dvwa';
$_DVWA['db_password'] = 'dvwa';
Save and exit (CTRL+O, CTRL+X).

---

🔄 Step 6: Restart Apache
Restart Apache to apply configuration changes:

bash
Copy code
sudo systemctl restart apache2
🌍 Step 7: Access DVWA
Open a browser in Kali and go to:

---

Login using:

Username: admin

Password: password

Navigate to DVWA Security → Set Security Level → Choose Low for initial practice.

---

🧪 Final Lab Topology
Machine	Role	IP Address	Network Mode
Kali Linux	Attacker	192.168.XXX.10	Host-Only / NAT
DVWA (on Kali)	Web Target	127.0.0.1	Localhost

---

🔒 Safety Notes
Use Host-Only or NAT network mode to keep your lab isolated.

Take VM snapshots to roll back after exploitation.

Do NOT expose DVWA to the internet.

---

✅ DVWA setup is complete!
You can now safely practice:

SQL Injection

XSS (Cross-Site Scripting)

Command Injection

File Upload vulnerabilities

Brute-Force attacks

CSRF and more…

Happy Hacking! 🎯
