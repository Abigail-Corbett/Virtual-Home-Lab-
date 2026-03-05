# Virtual-Home-Lab

## Project Overview
This repository documents the architecture and execution of a localized cybersecurity laboratory. The main objective was to simulate a controlled environment for practicing penetration testing methodologies, vulnerability assessment, and secure network configuration.

## Tech Stack
* **Virtualization:** Oracle VirtualBox
* **Attacker OS:** Kali Linux
* **Victim OS:** Metasploitable 2
* **Networking:** Host-Only Adapter (Isolated environment for maximum safety)

---

## Lab Architecture
The lab consists of two virtual machines connected via a virtualized private network to ensure no traffic escapes to the public internet.

* **K-Node-01** (Attacker) --> Kali Linux
* **M-Node-02** (Victim) --> Metasploitable 2

---

## Key Learning Objectives & Achievements
* **Environment Virtualization:** Configured and managed multiple virtual instances using VirtualBox.
* **Network Engineering:** Established an isolated "Host-Only" subnet to simulate a private enterprise network.
* **System Verification:** Verified shell integrity and user privileges via Command Line Interface (CLI).

---

## Documentation & Execution

### 1. Virtual Machine Provisioning
Successfully downloaded and created the two virtual machines.

<img width="566" height="314" alt="VirtualBox Manager View" src="https://github.com/user-attachments/assets/b96176e0-81f6-475f-b43b-f32c2ed36090" />

### 2. Environment Initialization
Initialized the Kali Linux 2025.4 virtual instance via Oracle VirtualBox, confirming the integrity of the virtual appliance import process. Utilized the `whoami` command to verify current user privileges and ensure that the shell environment was correctly initialized.

<img width="682" height="430" alt="Kali Terminal Verification" src="https://github.com/user-attachments/assets/393c9363-238f-4190-af1a-9d11be6c6239" />

> **Note:** By verifying the environment with a basic terminal command like `whoami`, I established a baseline for the system's state before moving into network reconnaissance. Operating within a Host-Only network ensures that all future testing is contained within a secure, private sandbox, preventing unauthorized traffic from reaching the Local Area Network (LAN).

### 3. Connectivity Testing
I successfully deployed the Metasploitable 2 node and utilized the `ifconfig` command to identify the target IP address within the local subnet. I then verified the connection between the two machines using the Kali Linux command:
`ping [target_ip_address]`

---

## Troubleshooting & Lab Maintenance

### **Issue: Dynamic Host Configuration Protocol (DHCP)**
* **Problem:** After moving the victim node from a NAT configuration to a Host-Only Adapter, the operating system kept the previous IP address, which prevented communication with the attacker node.
* **Solution:** Performed a manual DHCP renewal (forcing the computer to ask for new network info) using the following commands:
 ```bash
    sudo dhclient -r eth0
    sudo dhclient eth0
```
* **Result** Successfully obtained a new IP address, enabling "ping" requests between nodes.

### System Integrity Procedure
To prevent filesystem corruption, all nodes follow a strict Graceful Shutdown protocol:

* **Metasploitable 2**: ```bash sudo shutdown -h now ```

* **Kali Linux**: Selected "Shut Down" from the application menu.

---

 ## Future Roadmap
* **Network Reconnaissance**: Use Nmap scans to identify open ports and services on the victim node.

* **Vulnerability Analysis**: Map discovered services to known Common Vulnerabilities and Exposures (CVE).
* **Log Monitoring**: Implement a SIEM to track attack traffic.

---

## Author 
Abigail Corbett 
