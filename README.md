
# 🔐 Kali Linux Penetration Testing Lab Setup

<p align="center">
  <b>Cybersecurity Internship – Virtual Penetration Testing Environment</b><br>
  
</p>

---

## 📌 Overview

This project documents the setup of a controlled **Kali Linux penetration testing laboratory** using **Oracle VirtualBox**.

The environment is designed for cybersecurity learning, network reconnaissance, vulnerability assessment, web security testing, packet analysis, and other authorized security exercises.

> ⚠️ **Disclaimer:** This lab is intended for educational and authorized security testing only. Do not scan, attack, or test systems without explicit permission from the owner.

---

## 🏗️ Lab Architecture

```text
                         🌐 Internet
                              │
                              │
                    ┌─────────▼─────────┐
                    │    Windows 10     │
                    │      Host OS      │
                    └─────────┬─────────┘
                              │
                       Oracle VirtualBox
                              │
                    ┌─────────▼─────────┐
                    │    NatNetwork     │
                    │   10.0.0.0/24     │
                    │ Gateway: 10.0.0.1 │
                    └─────────┬─────────┘
                              │
                    ┌─────────▼─────────┐
                    │    Kali Linux     │
                    │      2026.2       │
                    │  IP: 10.0.0.2/24  │
                    │  DNS: 8.8.8.8     │
                    └───────────────────┘
```

---

## 💻 Lab Specifications

| Component | Configuration |
|---|---|
| Host Operating System | Windows 10 |
| Virtualization Platform | Oracle VirtualBox |
| Security Operating System | Kali Linux 2026.2 |
| Architecture | AMD64 / x64 |
| Network Mode | NAT Network |
| NAT Network Name | `NatNetwork` |
| IPv4 Network | `10.0.0.0/24` |
| Kali Linux IP | `10.0.0.2/24` |
| Gateway | `10.0.0.1` |
| DNS Server | `8.8.8.8` |
| Network Adapter | Intel PRO/1000 MT Desktop (82540EM) |
| Security Tools | Burp Suite, Wireshark, Nmap |

---

# 🚀 Installation & Configuration

## 1. Install Oracle VirtualBox

Install Oracle VirtualBox on the Windows host machine.

After installation:

1. Launch **Oracle VirtualBox Manager**.
2. Verify that VirtualBox is working correctly.
3. Prepare the Kali Linux virtual machine.

   

---

## 2. Obtain Kali Linux VirtualBox Image

Download the appropriate **Kali Linux VirtualBox image**.

The lab uses:

```text
kali-linux-2026.2-virtualbox-amd64
```

Extract the downloaded archive if required.

---

## 3. Import Kali Linux into VirtualBox

In Oracle VirtualBox:

```text
File → Import Appliance
```

Select the Kali Linux VirtualBox appliance and import it.

Recommended resources:

- RAM: 4 GB or more
- CPU: 2 cores or more
- Storage: 20 GB or more
- Network Adapter: Enabled

After importing, select the Kali VM and click **Start**.

---

## 4. Boot Kali Linux

After starting the VM, log in to Kali Linux.

The successful desktop environment confirms that the virtual machine has booted correctly.
<img width="1915" height="1012" alt="Kali Network set" src="https://github.com/user-attachments/assets/3df9261a-235c-4f06-91dd-1cc3152d6d8b" />


---

# 🌐 5. Create the Custom NAT Network

Open:

```text
VirtualBox → Network → NAT Networks
```

Create a new NAT Network with:

```text
Name:        NatNetwork
IPv4 Prefix: 10.0.0.0/24
DHCP:        Enabled
```

The `/24` subnet corresponds to:

```text
255.255.255.0
```



<img width="1911" height="1012" alt="NAT Set" src="https://github.com/user-attachments/assets/8e9cc410-2e56-45e7-a12b-bfbcb3348164" />


---

# 🔌 6. Configure Kali Network Adapter

Open:

```text
Kali Linux VM
→ Settings
→ Network
→ Adapter 1
```

Configure:

```text
Enable Network Adapter: ✓
Attached to:            NAT Network
Name:                   NatNetwork
Adapter Type:           Intel PRO/1000 MT Desktop (82540EM)
Virtual Cable Connected: ✓
```


---

# 📡 7. Configure Static IP Address

Inside Kali Linux, open the wired network connection settings.

Navigate to:

```text
IPv4 Settings
```

Set:

```text
Method: Manual

Address:   10.0.0.2
Netmask:   24
Gateway:   10.0.0.1
DNS:       8.8.8.8
```

### Configuration Table

| Setting | Value |
|---|---|
| IPv4 Method | Manual |
| IP Address | `10.0.0.2` |
| Netmask | `24` |
| Gateway | `10.0.0.1` |
| DNS | `8.8.8.8` |

Click **Save** after entering the values.

<img width="1272" height="791" alt="Wired c1" src="https://github.com/user-attachments/assets/d2eb9bc4-3c9e-478b-a283-00f451b9927d" />


---

# 🔎 8. Verify Network Configuration

Open the Kali terminal.

### Check IP Address

```bash
ip addr
```

Expected:

```text
10.0.0.2/24
```

### Check Routing Table

```bash
ip route
```

A default route through `10.0.0.1` should be present.

### Test Gateway

```bash
ping -c 4 10.0.0.1
```

### Test Internet Connectivity

```bash
ping -c 4 8.8.8.8
```

### Test DNS Resolution

```bash
ping -c 4 google.com
```

Successful responses confirm that the network configuration is functioning correctly.

---

# 🦈 9. Configure Wireshark

Wireshark is used for packet capture and network traffic analysis.

Launch:

```text
Applications → Wireshark
```

Select the active interface, such as:

```text
eth0
```

Start a capture and generate test traffic:

```bash
ping -c 4 8.8.8.8
```

The packets generated by the test should appear in Wireshark.

<img width="1272" height="796" alt="Wire" src="https://github.com/user-attachments/assets/85316179-f4f6-4a5a-907e-a4473a56d5b2" />


---

# 🕵️ 10. Configure Burp Suite

Burp Suite is used for authorized web application security testing.

Launch:

```text
Applications → Web Application Analysis → Burp Suite
```

The lab uses:

```text
Burp Suite Community Edition
```

For a temporary lab project, select:

```text
Temporary project in memory
```

Then click:

```text
Next
```

<img width="1272" height="787" alt="Burp" src="https://github.com/user-attachments/assets/2ffca0e3-8b9b-46ff-9172-8f99bac94847" />


---

# 💾 11. Create a VirtualBox Snapshot

After successfully configuring Kali Linux and verifying network connectivity, create a clean snapshot.

Navigate to:

```text
VirtualBox
→ Kali Linux VM
→ Snapshots
→ Take
```

Recommended snapshot name:

```text
My Fresh Kali Linux
```

Example description:

```text
Kali Linux network configuration completed successfully.
Static IP configured and Internet connectivity verified.
```

The snapshot provides a restore point that can be used if the lab becomes misconfigured during future testing.

<img width="1277" height="796" alt="Kali Home" src="https://github.com/user-attachments/assets/da122965-163a-488a-a228-690470d69a6e" />


---

# 🛠️ Tools Used

| Tool | Purpose |
|---|---|
| **Kali Linux** | Cybersecurity and penetration-testing platform |
| **Oracle VirtualBox** | Virtualization and lab isolation |
| **Wireshark** | Network packet capture and analysis |
| **Burp Suite** | Web application security testing |
| **Nmap** | Network discovery and service enumeration |

---

# 🔐 Security & Ethical Use

This environment should be used as a **controlled cybersecurity laboratory**.

Only perform security testing against:

- Systems you own
- Intentionally vulnerable lab machines
- Training platforms
- Targets for which you have explicit authorization

Never use these tools to access, disrupt, or test unauthorized systems.

---

# 📊 Expected Final Configuration

```text
Host OS
└── Windows 10
    │
    └── Oracle VirtualBox
        │
        └── Kali Linux 2026.2
            │
            ├── Network: 10.0.0.0/24
            ├── IP:      10.0.0.2/24
            ├── Gateway: 10.0.0.1
            ├── DNS:     8.8.8.8
            │
            ├── Burp Suite
            ├── Wireshark
            └── Nmap
```

---

# 📁 Repository Structure

```text
kali-linux-pentest-lab/
│
├── README.md
│
├── screenshots/
│   ├── 1-screenshot-title-image.png
│   ├── Kali Home.png
│   ├── NAT Set.png
│   ├── Kali Network set.png
│   ├── Wired c1.png
│   ├── Wire.png
│   ├── Burp.png
│   └── Snapshot.png
│
└── documentation/
    └── lab-notes.md
```

> **Note:** Keep the screenshot filenames exactly as referenced above, or update the image paths in this README if you rename them.

---

# 🎯 Learning Outcomes

By completing this lab, the following practical skills are developed:

- Virtual machine deployment
- Kali Linux configuration
- VirtualBox network configuration
- NAT Network creation
- IPv4 addressing and subnetting
- Static IP configuration
- Gateway and DNS configuration
- Network connectivity troubleshooting
- Packet capture with Wireshark
- Web security testing with Burp Suite
- Virtual machine snapshot and recovery
- Secure and controlled penetration-testing practices

---

## 👨‍💻 Author

Aarti Javiya

Cybersecurity Internship – Networkwalks 

Batch083 

---

## ⭐ Conclusion

The Kali Linux penetration-testing laboratory was successfully deployed using Oracle VirtualBox. A custom `10.0.0.0/24` NAT Network was created, and Kali Linux was configured with the static address `10.0.0.2/24`, gateway `10.0.0.1`, and DNS `8.8.8.8`.

Connectivity was verified, security tools such as Wireshark and Burp Suite were configured, and a clean VirtualBox snapshot was created. The resulting environment provides a controlled foundation for authorized cybersecurity experiments and penetration-testing exercises.
