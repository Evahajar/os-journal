
# Week 1: System Planning & Distribution Selection

<div style="display:flex; gap:10px; margin-top:20px;"> <a href="index.html" style=" background:#f4d7e3; padding:10px 18px; color:#5a3a45; border-radius:8px; text-decoration:none; border:1px solid #e7bdcc; font-weight:600;"> ⬅ Back to Home </a> <a href="week2.html" style=" background:#f4d7e3; padding:10px 18px; color:#5a3a45; border-radius:8px; text-decoration:none; border:1px solid #e7bdcc; font-weight:600;"> ➡ Go to Week 2 </a> </div>

---

## 1. System Architecture Diagram

![System Architecture Diagram](images/diagram.png)

The project uses a **small virtualised environment** built on my Windows laptop.
The setup consists of:

* **One server VM:** Ubuntu Server 24.04.3 LTS
* **One workstation VM:** Debian 13 (Trixie)

Both virtual machines run inside **VirtualBox** using **Bridged Networking**, allowing them to obtain real LAN IP addresses from the router and communicate as if they were physical devices on the same network.

---

### Architecture Overview

#### Host Machine (Windows Laptop)

* Runs Oracle VirtualBox
* Manages both virtual machines
* Connected to the local LAN (e.g. `192.168.1.x`)

#### Server VM – Ubuntu Server 24.04.3 LTS

* **IP Address:** `192.168.1.221`
* **Installed services:**

  * OpenSSH
  * Apache2
  * UFW Firewall
  * Fail2Ban
  * AppArmor
* Runs in **headless mode** (no desktop environment)

#### Workstation VM – Debian 13 (Trixie)

* **IP Address:** `192.168.1.183`
* Used to compare distributions and test connectivity
* Lightweight GUI for easier workstation usage

---

## 2. Distribution Selection & Justification

For the server environment, **Ubuntu Server 24.04.3 LTS** was selected based on its stability, security features, and documentation quality, as well as its widespread use in industry and cloud platforms.

To justify this choice, Ubuntu Server was compared with **Debian**, which was installed as the workstation VM.

### Ubuntu Server 24.04 LTS – Rationale

* Long-Term Support (5 years + extended security maintenance)
* Large package repositories and strong community documentation
* Beginner-friendly while still used professionally
* Secure defaults:

  * UFW firewall
  * AppArmor
  * Unattended security updates
* Suitable for learning real-world server administration

### Debian 13 (Trixie) – Alternative Distribution

Debian is known for:

* Exceptional stability
* Conservative software updates
* Strong reliability in enterprise systems
* Fully community-driven development

### Distribution Comparison

| Feature          | Ubuntu Server          | Debian                |
| ---------------- | ---------------------- | --------------------- |
| Release Cycle    | Regular LTS releases   | Slow, stability-first |
| Default Security | UFW + AppArmor         | Manual configuration  |
| Package Versions | Newer, more up to date | Older but very stable |
| Support          | Canonical + community  | Community-based only  |
| Learning Curve   | Easier for beginners   | More manual setup     |

### Conclusion

Ubuntu Server was better suited for this coursework due to its faster setup, secure defaults, and accessible documentation. Debian remains an excellent choice for workstation use, but Ubuntu provides a smoother experience for server-focused tasks.

---

## 3. Workstation Configuration Decision

The workstation VM uses **Debian 13 (Trixie)** for the following reasons:

* Lightweight GUI and low resource usage
* High compatibility with VirtualBox
* Stable and predictable behaviour
* Effective client system when connecting to Ubuntu Server
* Enables comparison between two major Linux distributions (Debian vs Ubuntu)

Debian provides a clean environment for running Linux commands, testing networking, and analysing logs without unnecessary overhead.

---

## 4. Network Configuration Documentation

Both virtual machines use **Bridged Adapter mode** in VirtualBox.

This configuration allows:

* Each VM to appear as a separate device on the local network
* Automatic IP assignment via DHCP
* Realistic server–client communication

### Purpose of Bridged Networking

* SSH access from host to server
* Testing web services via browser
* Simulating a real-world network environment

### Ubuntu Server Network Output (`ip addr`)

![Ubuntu IP](images/ip.png)

**Observed:**

* Interface: `enp0s3`
* IPv4 Address: `192.168.1.221`
* Confirms bridged networking is active

### Debian Workstation Network Output (`ip addr`)

![Debian IP](images/ip1.png)

**Observed:**

* IPv4 Address: `192.168.1.183`
* Same subnet as the server VM

This confirms both systems are correctly configured for coursework tasks.

---

## 5. System Specifications Using CLI (Verification Evidence)

System verification was completed using the required command-line tools.

### Kernel & Architecture

```bash
uname -a
```

![uname output](images/sysinfo.png)

Confirms a 64-bit Linux kernel running on `x86_64` architecture.

---

### Memory Usage

```bash
free -h
```

![Memory Usage](images/memoryusage.png)

* Total RAM: ~1.9 GB
* Used: ~347 MB
* Swap: Disabled

This confirms the system is lightweight and efficient.

---

### Disk Usage

```bash
df -h
```

![Disk Usage](images/diskusage.png)

* Total Disk: 25 GB
* Used: ~12%
* Free: ~21 GB

---

### Network Configuration

```bash
ip addr
```

![IP address](images/ip.png)

Confirms the bridged interface and IPv4 address `192.168.1.221`.

---

### Operating System Verification

```bash
lsb_release -a
```

![OS Release](images/osrelease.png)

Confirms **Ubuntu Server 24.04.3 LTS (Noble)**.

---

## Debian Workstation – System Specifications

### Kernel

```bash
uname -a
```

![uname Debian](images/uname1.png)

### Memory

```bash
free -h
```

![free Debian](images/free.png)

### Disk

```bash
df -h
```

![df Debian](images/dfh.png)

### OS Release

```bash
lsb_release -a
```

![release Debian](images/release.png)

---

## Reflection

This week involved building a complete virtual environment from scratch and understanding the differences between server and workstation Linux distributions. Installing and configuring two different systems enabled direct comparison and highlighted how design choices, such as update frequency and security defaults, influence real-world server administration.
