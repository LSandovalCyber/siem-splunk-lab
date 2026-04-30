# 🔍 SIEM Lab – Splunk Deployment & Log Analysis

## 📌 Overview

This project demonstrates the deployment of a Security Information and Event Management (SIEM) system using Splunk on an Ubuntu server within a virtualized lab environment.

The lab is designed to simulate centralized log collection and analysis, allowing for monitoring, investigation, and detection of system activity across a domain environment.

---

## 🧱 Lab Environment

| System              | Role                   | IP Address     |
| ------------------- | ---------------------- | -------------- |
| Windows Server 2022 | Domain Controller (DC) | 192.168.56.10  |
| Windows 10 Client   | Domain-joined Machine  | 192.168.100.10 |
| Ubuntu Linux        | SIEM Server (Splunk)   | 192.168.56.20  |

* **Platform:** VirtualBox
* **Network Type:** Internal Network + NAT (Ubuntu)
* **Domain:** lab.local

---

## 🎯 Objectives

* Configure Ubuntu with dual-network interfaces (Internal + NAT)
* Install and configure Splunk Enterprise on Ubuntu
* Establish centralized log collection from Windows systems
* Analyze authentication events within Splunk
* Simulate and detect suspicious login activity
* Develop foundational SIEM and SOC analyst skills

---

## ⚙️ Configuration

### Network Setup

* Configured Ubuntu with:

  * Internal Network for lab communication
  * NAT adapter for internet access
* Resolved network configuration issues using Netplan
* Ensured DHCP assignment for NAT interface

---

### Splunk Installation

```bash id="y3c1wx"
cd ~/Downloads
sudo dpkg -i splunk*.deb
sudo /opt/splunk/bin/splunk start
```

* Accepted license agreement
* Created administrative credentials
* Accessed Splunk Web Interface via:

```plaintext id="8p2w6x"
http://localhost:8000
```

---

## 🧪 Validation

✔ Ubuntu successfully connected to internet via NAT
✔ Internal network communication maintained with lab systems
✔ Splunk installed and running on Ubuntu
✔ Splunk web interface accessible
✔ System ready for log ingestion and analysis

---

## 📸 Screenshots

![Splunk Installation](screenshots/01-splunk-install.png)

*Splunk successfully installed on Ubuntu*

![Splunk Web Interface](screenshots/02-splunk-login.png)

*Accessing Splunk web interface*

Additional screenshots available in the [screenshots directory](screenshots/).

---

## 📚 Skills Demonstrated

* Linux system configuration and networking
* Netplan configuration and troubleshooting
* SIEM deployment (Splunk Enterprise)
* Understanding of centralized logging architecture
* Troubleshooting network and service configuration issues

---

## 🚧 Project Status

* [x] Ubuntu network configuration (Internal + NAT)
* [x] Internet connectivity established
* [x] Splunk installation completed
* [ ] Log ingestion from Windows systems
* [ ] Event search and analysis
* [ ] Detection use cases

---

## 🚀 Next Steps

* Configure Splunk Forwarder on Windows systems
* Ingest Windows Event Logs into Splunk
* Create search queries for authentication events
* Simulate brute-force login attempts
* Build detection queries and alerts

---

## 🔧 Troubleshooting

### Issue: Loss of network connectivity after reboot

**Symptoms:**

* No IPv4 address assigned to interfaces
* NAT adapter not receiving DHCP address
* Unable to reach external networks

**Root Cause:**

* Netplan configured with incorrect renderer (`NetworkManager`)
* System was using `systemd-networkd`

**Solution:**

* Updated Netplan configuration:

```yaml id="0mnk0t"
network:
  version: 2
  renderer: networkd
  ethernets:
    enp0s3:
      dhcp4: no
      addresses:
        - 192.168.56.20/24
    enp0s8:
      dhcp4: yes
```

```bash id="8wrtjv"
sudo netplan try
```

**Result:**

* Internal network restored
* NAT interface received IP (10.0.x.x)
* Internet connectivity successfully re-established

---

## 🧠 Key Takeaway

* Successfully deployed a SIEM environment using Splunk in a virtual lab
* Gained hands-on experience with Linux networking and troubleshooting
* Understood how centralized logging enables security monitoring
* Learned how misconfigured network services impact system connectivity
* Established a foundation for real-world SOC analyst workflows
