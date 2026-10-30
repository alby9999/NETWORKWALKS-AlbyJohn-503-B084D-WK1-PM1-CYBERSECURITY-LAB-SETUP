# 🛡️ Cybersecurity Lab Setup – Kali Linux

> **Building my own cybersecurity practice environment using Kali Linux and VirtualBox.**

## 📌 About the Project

As part of my cybersecurity learning, I wanted to set up a small virtual lab where I could safely experiment with Linux, networking, and future ethical hacking exercises.

For this setup, I used **Kali Linux inside Oracle VirtualBox** and configured a separate NAT Network so the virtual machine could communicate with the internet while keeping the lab environment organized.

This repository documents the setup and the configuration I completed.

---

## ⚙️ Lab Setup

**Host:** Windows  
**Virtual Machine:** Kali Linux  
**Virtualization:** Oracle VirtualBox

### Network Configuration

| Setting | Configuration |
|---|---|
| Network Name | `KaliLab` |
| Network | `10.0.0.0/24` |
| Gateway | `10.0.0.1` |
| Kali IP | `10.0.0.2/24` |
| DHCP | Disabled |
| DNS | `8.8.8.8`, `1.1.1.1` |

---

## 🔧 What I Configured

### 1. Kali Linux in VirtualBox

Imported the Kali Linux VirtualBox image and configured it as the main machine for the cybersecurity lab.

**VM:** `kali-linux-2026.3-virtualbox-amd64`

📸 *Screenshot: Kali Linux running in VirtualBox*
<img width="1600" height="848" alt="WhatsApp Image 2026-10-30 at 1 32 34 AM" src="https://github.com/user-attachments/assets/5f3149b7-66e6-4edb-8561-50fc8c43ee30" />

---

### 2. Custom Network

Created a VirtualBox NAT Network called `KaliLab` using:

```text
10.0.0.0/24
```

Kali Linux was assigned the static IP:

```text
10.0.0.2/24
```

This gives the lab a fixed network setup that can later be expanded with additional virtual machines.

---

### 3. Internet Access

After configuring the network, I tested the connection from Kali using:

```bash
ping -c 4 8.8.8.8
```

and:

```bash
ping -c 4 google.com
```

Both tests confirmed that the Kali VM could access the internet.

📸 *Screenshot: Web browsing from Kali Linux*
<img width="1600" height="849" alt="WhatsApp Image 2026-10-30 at 1 32 35 AM" src="https://github.com/user-attachments/assets/2018fd96-bcda-4b3e-b162-af30c888a28f" />

---

### 4. Shared Folder

I also configured a shared folder between Windows and Kali Linux.

**Windows:**

```text
C:\downloads
```

**Kali Linux:**

```text
/media/sf_downloads
```

This makes it easier to move files between the Windows host and the Kali virtual machine during future labs.

📸 *Screenshot: Files shared between Windows and Kali Linux*
<img width="902" height="225" alt="image" src="https://github.com/user-attachments/assets/61758186-7adc-4a4a-9cb4-4d474cfaa26f" />

---

### 5. Clipboard & Drag and Drop

Enabled:

- ✅ Bidirectional Clipboard
- ✅ Bidirectional Drag and Drop

This makes working between Windows and Kali much easier during practical exercises.

---

### 6. Snapshot

Once everything was working, I created a **VirtualBox snapshot** of the completed Kali setup.

This gives me a clean restore point before starting future cybersecurity labs.

---

## 📸 Setup Proof
<img width="1682" height="936" alt="image" src="https://github.com/user-attachments/assets/3c36c960-3215-41aa-b9cc-f441dd64bab0" />

The repository includes screenshots showing:

- 🖥️ Kali Linux running in VirtualBox
- 📁 Shared files between Windows and Kali
- 🌐 Internet browsing from Kali Linux
- ⚙️ Completed lab environment

These screenshots show the setup working rather than just describing the configuration.

---
## 🛠️ Problems I Faced & How I Fixed Them

Setting up the lab wasn't completely smooth, and I had to troubleshoot a few things along the way. These problems actually helped me understand the setup better.

### 🌐 Websites weren't opening in Kali

At first, Kali had internet access when I tested it from the terminal, but websites weren't opening properly in Firefox.

I checked the Firefox network settings and found that a proxy was enabled. I changed it to **No Proxy**, and the browser started working normally.

**What I learned:** Internet access can work in the terminal while a browser still has its own network configuration issue.

---

### 📁 Shared folder wasn't accessible at first

I created the shared `downloads` folder in VirtualBox, but it wasn't immediately available to my Kali user.

I fixed this by adding the `kali` user to the `vboxsf` group:

```bash
sudo usermod -aG vboxsf kali
```

After restarting Kali, I could access the folder at:

```text
/media/sf_downloads
```

**What I learned:** Linux permissions and user groups matter when working with shared resources.

---

### 🌐 Setting up the static IP

The lab required Kali to use a specific IP address instead of getting one automatically.

I configured the network manually and assigned Kali:

```text
IP:       10.0.0.2/24
Gateway:  10.0.0.1
DNS:      8.8.8.8 / 1.1.1.1
```

I then used `ping` to make sure the connection was working.

**What I learned:** This gave me some practical experience with IP addresses, gateways, DNS, and basic network troubleshooting.

---

### 📦 VirtualBox VM registration issue

While working with the Kali VM, I also ran into a VirtualBox issue where the VM was already registered, causing a duplicate UUID/import problem.

Instead of importing another copy, I continued using the Kali VM that was already registered in VirtualBox.

**What I learned:** VirtualBox uses unique identifiers for virtual machines, so trying to register the same VM again can cause conflicts.

---

### 💾 Creating a safe restore point

Before moving on to future cybersecurity labs, I wanted to make sure I had a working version of Kali that I could return to if something went wrong.

Once everything was working, I created a VirtualBox snapshot.

---
## 🧠 What I Learned
Taking a snapshot before experimenting can save a lot of time because I can return to a known working setup instead of configuring everything again.
This lab was more than just installing Kali Linux. Setting everything up myself helped me understand how the different parts of a cybersecurity lab fit together.

A few things I learned along the way:

- How to set up and manage a **virtual machine using VirtualBox**.
- How a **NAT Network** works and how to create one for a lab environment.
- How **IP addresses, subnets, gateways, and DNS** are used when configuring a network.
- How to give Kali Linux a **static IP address** and check whether the configuration is working.
- How to use basic Linux commands such as `ping`, `ip addr`, and `ip route` to check network connectivity.
- How to share files between my **Windows system and Kali Linux**.
- How Linux **user groups and permissions** affect access to shared folders.
- How VirtualBox features like **clipboard sharing and drag-and-drop** make working between the host and VM easier.
- Why taking a **snapshot** before starting practical work is useful.

The biggest thing I took away from this lab is that setting up a cybersecurity environment isn't just about installing Kali and opening some tools. Understanding the **network, connectivity, file sharing, and VM configuration** is an important part of building a useful lab.
---

## 🚀 What's Next?

This gives me a good starting point for the cybersecurity labs and practical exercises I want to work on next.
The lab can later be expanded with additional virtual machines and used for:

- Network security practice
- Linux and networking experiments
- Ethical hacking labs
- CTF challenges
- Vulnerability testing in controlled environments

The goal is to gradually build a practical cybersecurity lab and learn by actually working with the environment.

---

## ⚠️ Disclaimer

This lab is created for **educational purposes and authorized cybersecurity practice only**.
Any security testing should only be performed on systems and networks where you have permission.

---

## 📚 Reference

Setup based on the **WK1-PM1 – Week 1: Project Module 1 – Lab Setup VirtualBox and Kali Linux** lab material.

---
## 📌 Project Information

| **Field** | **Details** |
| --------- | ----------- |
| Author    | Alby John |
| Project   | Essentials of Cybersecurity & Penetration Testing |
| Module    | WK1-PM1 |
| Tools     | Kali Linux 2026.3, Oracle VirtualBox 7.2.22 |
