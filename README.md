🛡️ Kali Linux Virtual Lab Setup on VMware Workstation (Windows 11 Host)

## 📖 Project Overview
This repository documents the step-by-step process I followed to set up a **personal cybersecurity lab** using **Kali Linux** as a virtual machine on my **Windows 11 system** with **VMware Workstation Player** (default configuration).

The primary goal of this lab is to build a controlled environment for practicing **penetration testing**, **SOC analysis**, and **GRC projects** as part of my cybersecurity learning journey.

---

## 🖥️ Host Machine Specifications

| Specification | Details |
|---------------|---------|
| Operating System | Windows 11 |
| RAM | Minimum 8 GB |
| Processor | Intel i5 / AMD Ryzen equivalent |
| Storage | At least 50 GB free space |

---

## 📥 Tools and Resources Used

| Tool | Source | Notes |
|-----|------|------|
| Kali Linux ISO | [https://www.kali.org/get-kali/](https://www.kali.org/get-kali/) | Latest stable release |
| VMware Workstation Player | [TechSpot Download Link](https://www.techspot.com/downloads/downloadnow/189/?evp=f14a48a23bc560f5fbe81b8d83387b41&file=11957) | Free version |
| VMware Tools (Optional) | Default from Kali | Improves performance |

---

## 🛠️ Step-by-Step Walkthrough

### ✅ 1. Download Kali Linux ISO
- Navigated to [kali.org](https://www.kali.org/get-kali/).
- Downloaded the latest **Kali Linux ISO** for Virtual Machines.

### ✅ 2. Install VMware Workstation Player
- Installed VMware Workstation Player using a referral link provided by my mentor.
- Selected default installation options.

### ✅ 3. Create a New Virtual Machine (Default Mode)
- Selected **"Typical (Recommended)"** during VM creation.
- Chose the downloaded **Kali Linux ISO** as the installation source.
- Allocated default resources:
  - CPU: 1 Core
  - RAM: 2 GB
  - Disk: 20 GB (Dynamically allocated)
  - Network: NAT mode (default)

### ✅ 4. Install Kali Linux on VMware
- Followed the on-screen Kali installer.
- Accepted all default settings (disk partitioning, user creation, etc.).
- Created a default user with a strong password.

### ✅ 5. First Boot and Updates
- Successfully booted into the **Kali Linux Desktop Environment (XFCE by default)**.
- Ran system update commands:
  ```bash
  sudo apt update && sudo apt upgrade -y
