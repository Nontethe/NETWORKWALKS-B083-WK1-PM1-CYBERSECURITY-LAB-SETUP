# NETWORKWALKS-B083-WK1-PM1-CYBERSECURITY-LAB-SETUP
A controlled cybersecurity testing laboratory built using VirtualBox and Kali Linux. The environment uses an isolated 10.0.0.0/24 NAT Network, with Kali Linux configured as the primary security-testing machine at 10.0.0.2/24 with Internet access.The environment provides a safe foundation for practicing network reconnaissance, vulnerability assessment, penetration testing, and other authorized cybersecurity activities.

# 🔐 Cybersecurity & Penetration Testing Lab

## 📌 Project Overview

This project documents the creation of a controlled cybersecurity testing environment using **Oracle VirtualBox** and **Kali Linux**.

The objective is to build an isolated virtual network that can be used for cybersecurity training, reconnaissance, vulnerability testing, and penetration-testing exercises against systems that are intentionally deployed for testing.

The environment is designed so that additional virtual machines can be connected to the same laboratory network in future projects.

> ⚠️ **Ethical Use:** This environment is intended for educational and authorized security testing only. Never use the techniques or tools from this lab against systems without explicit permission.

---

## 🎯 Project Objectives

The main goals of this project were to:

* Install and configure VirtualBox.
* Deploy Kali Linux as the cybersecurity testing machine.
* Create a dedicated VirtualBox NAT Network.
* Configure the virtual network using `10.0.0.0/24`.
* Assign Kali Linux the static address `10.0.0.2/24`.
* Provide Kali Linux with Internet connectivity.
* Enable clipboard sharing between the host and VM.
* Enable drag-and-drop functionality.
* Configure a shared '/downloads' folder.
* Verify IP addressing and network connectivity.
* Create a clean VM snapshot for future recovery.
* Document the completed laboratory environment.

---

# 🏗️ Laboratory Architecture

The laboratory uses a VirtualBox NAT Network to provide connectivity between the virtual machines while allowing outbound Internet access.

```text
                       INTERNET
                           │
                           │
                    ┌──────┴──────┐
                    │ Host Machine│
                    │   Windows   │
                    └──────┬──────┘
                           │
                    VirtualBox NAT
                       Network
                    10.0.0.0/24
                           │
                    ┌──────┴──────┐
                    │  Kali Linux │
                    │ 10.0.0.2/24 │
                    │   Attacker  │
                    └─────────────┘
```

Additional target machines can be connected to the same NAT Network later.

---

# ⚙️ Environment Configuration

| Component             | Configuration          |
| --------------------- | ---------------------- |
| Host Operating System | Windows 10             |
| Hypervisor            | VirtualBox 7.2         |
| Security Testing OS   | Kali Linux 2026.2      |
| Kali Memory           | 2048 MB                |
| Virtual Network       | NAT Network            |
| Network Name          | `NatNetwork`           |
| Network CIDR          | `10.0.0.0/24`          |
| Kali IP Address       | `10.0.0.2/24`          |
| Subnet Mask           | `255.255.255.0`        |
| Default Gateway       | `10.0.0.1`             |
| DNS Server            | `8.8.8.8`              |
| Future Lab IP Range   | `10.0.0.3 - 10.0.0.99` |
| Internet Access       | Enabled                |

---

# 🧰 Software Used

The following software was used to create the environment:

* **Oracle VirtualBox** — virtualization platform
* **Kali Linux** — penetration-testing and cybersecurity distribution
* **7-Zip** — extraction of the Kali virtual-machine archive

---

# 🪜 Installation & Configuration

## 1. Install 7-Zip

7-Zip was installed to extract the Kali Linux virtual-machine archive.

The Kali VM package may be provided as a compressed `.7z` archive, so an archive utility is required before importing the machine into VirtualBox.

---

## 2. Install VirtualBox

VirtualBox was installed on the host computer and used as the virtualization platform for the cybersecurity laboratory.

After installation, hardware virtualization was checked to ensure that the computer supports virtualization.

Required BIOS/UEFI feature:

```text
Intel VT-x / AMD-V
```

---

## 3. Configure the NAT Network

A dedicated VirtualBox NAT Network was created for the laboratory.

### Network configuration

```text
Network Name:     NatNetwork
IPv4 Network:     10.0.0.0/24
IPv6:             Disabled
```

The `10.0.0.0/24` network provides 254 possible host addresses.

The Kali Linux VM uses:

```text
10.0.0.2
```

with the VirtualBox NAT gateway:

```text
10.0.0.1
```

The NAT Network was selected because it allows multiple laboratory VMs to communicate with one another while providing external network connectivity.

---

# 🐉 4. Import Kali Linux

The Kali Linux VirtualBox image was downloaded and imported into VirtualBox.

The first network adapter was configured as:

```text
Adapter 1:        Enabled
Attached to:      NAT Network
Network:          NatNetwork
Adapter Type:     Intel PRO/1000 MT Desktop
```

The Kali VM was allocated:

```text
Memory:           2048 MB
```

This VM acts as the primary security-testing machine in the laboratory.

---

# 📡 5. Configure Kali Network Settings

Kali Linux was configured with a static IPv4 address.

### IPv4 configuration

```text
IP Address:       10.0.0.2
Subnet Mask:      255.255.255.0
Gateway:          10.0.0.1
DNS:              8.8.8.8
```

The static address makes it easier to identify the Kali machine during future laboratory exercises.

The configuration can be checked from the Kali terminal with:

```bash
ip addr
```

and:

```bash
ip route
```
---

# 📂 7. Enable Drag and Drop

Drag-and-drop functionality was enabled in VirtualBox.

Configuration:

```text
Drag'n'Drop: Bidirectional
```

This provides an additional way of transferring files between the host and the Kali VM.

---

# 📁 8. Configure Shared `/downloads` Folder

A shared folder was created on the host machine for transferring laboratory files.

The VirtualBox shared-folder configuration was set to:

```text
Folder Name:      downloads
Auto-mount:       Enabled
Permanent:        Enabled
Read-only:        Disabled
```

The intended location inside Kali Linux is:

```text
/downloads
```

The shared directory can be checked from Kali using:

```bash
ls -la /downloads
```

This folder provides a convenient location for moving files required for authorized laboratory exercises.

---

# 🔎 9. Network Verification

After configuring the VM, several tests were performed to confirm that the laboratory was functioning correctly.

### Check Kali IP address

```bash
ip a
```

Expected address:

```text
10.0.0.2/24
```

### Check routing table

```bash
ip route
```

Expected default gateway:

```text
10.0.0.1
```

### Test the VirtualBox gateway

```bash
ping -c 4 10.0.0.1
```

Expected result:

```text
Successful replies
```

### Test Internet connectivity

```bash
ping -c 4 8.8.8.8
```

Expected result:

```text
Successful replies
```

### Test DNS resolution

```bash
nslookup networkwalks.com
```

Expected result:

```text
Domain successfully resolves
```

### Verify Nmap

```bash
nmap --version
```

Expected result:

```text
Nmap version information displayed
```

---

# 📸 Project Evidence

Screenshots documenting the configuration are included in this repository.

### Screenshot 1 — Project / Lab Environment

![Lab Setup](1-screenshot-title-image.png)

### Screenshot 2 — VirtualBox Network Configuration

![Network Configuration](2-screenshot-network-settings-1.png)

### Screenshot 3 — Kali Linux VM

![Kali Linux](3-screenshot-kali-linux.png)

### Screenshot 4 — Kali Network Configuration

![Kali Network](4-screenshot-kali-network-settings.png)

---

# 💾 10. Create a Baseline Snapshot

Once the installation and network configuration were completed, a clean VirtualBox snapshot was created.

Suggested snapshot name:

```text
Kali-Clean-Lab-Baseline
```

The snapshot provides a known-good recovery point.

Before performing future cybersecurity experiments, the VM can be restored to this state if a configuration becomes unstable or corrupted.

---

# 🧠 What I Learned

This project provided practical experience with several cybersecurity and virtualization concepts.

### 1. VirtualBox Networking

I learned how VirtualBox networking modes affect communication between virtual machines and external networks.

The NAT Network configuration is particularly useful for cybersecurity labs because multiple machines can share the same isolated virtual network.

### 2. IPv4 Addressing

The project provided hands-on experience configuring:

```text
IP address
Subnet mask
Default gateway
DNS
```

The laboratory uses:

```text
Network:   10.0.0.0/24
Kali:      10.0.0.2
Gateway:   10.0.0.1
```

### 3. Static Network Configuration

Using a predictable IP address makes it easier to reference the Kali machine during future scanning and testing exercises.

### 4. Virtual Machine Snapshots

I learned the importance of creating a clean baseline before performing security experiments.

A snapshot allows the VM to be returned to a known working state.

### 5. Laboratory Isolation

A dedicated virtual network provides a controlled environment where intentionally vulnerable machines can later be deployed for authorized testing.

### 6. Technical Documentation

I also learned that documenting configuration changes, verification commands, screenshots, and troubleshooting steps is an important part of professional cybersecurity work.

---

# 🔐 Security & Responsible Use

This laboratory is intended for:

* Cybersecurity education
* Penetration-testing practice
* Network-security experiments
* Vulnerability-assessment training
* Security-tool learning
* Testing intentionally vulnerable laboratory machines

All security testing must be performed against systems that you own or have explicit authorization to test.

Do not use these techniques against unauthorized systems, networks, websites, or devices.

---

# 🔮 Future Improvements

The laboratory can be expanded by adding additional virtual machines to the same network.

Possible future targets include:

```text
Kali Linux
10.0.0.2

        │
        │
   10.0.0.0/24
        │
   ┌────┴─────────────┐
   │                  │
Target VM          Windows VM
10.0.0.10         10.0.0.20
```

---

# 🔗 Resources

* 7-Zip: https://7-zip.org/download.html
* VirtualBox: https://virtualbox.org/wiki/Downloads
* Kali Linux: https://kali.org/get-kali

---

# 👤 Author

**[Nontethelelo Mahlangu]**
@Waqas  Harim
@Networkwalks

### Project Information

```text
Program:       Cybersecurity
Week:          01
Project:       Cybersecurity & Penetration Testing Lab
Platform:      GitHub
Environment:   VirtualBox + Kali Linux
Network:       10.0.0.0/24
```

---

## 📌 Repository Summary

An isolated cybersecurity laboratory created with VirtualBox and Kali Linux. The environment uses a `10.0.0.0/24` NAT Network, assigns Kali Linux the static address `10.0.0.2/24`, provides Internet access, and establishes the foundation for future authorized penetration-testing and cybersecurity exercises.
