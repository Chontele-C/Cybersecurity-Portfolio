\# 🔧 Linux Network Diagnostics Project (Ubuntu CLI)

This project demonstrates practical Linux networking diagnostics using only the command line on Ubuntu 22.04.    
It covers gathering IP/interface information, testing connectivity, DNS resolution, scanning remote hosts, and examining firewall rules — all documented with logs and screenshots.

\---

\#\# 🎯 Project Goal

\> To demonstrate practical proficiency in Linux command-line networking tools by diagnosing, analyzing, and documenting network configuration, connectivity, and security posture on a Ubuntu system — without relying on graphical interfaces.

\---

\#\# 📁 Project Structure

project-folder/  
 ├── logs/  
 │ ├── output.txt  
 │ ├── combined\_log.txt  
 │ └── network\_diagnostic\_session.txt  
 ├── screenshots/  
 │ ├── ip\_a.png  
 │ ├── ping\_google.png  
 │ └── ...  
 ├── README.md  
 └── Linux\_Network\_Diagnostics\_Project.pdf

`---`

`## 🧾 1. System Information & Interfaces`

`**Commands Used:**`  
```` ```bash ````  
`ip a`  
`ip route`  
`resolvectl status`  
`hostnamectl`

**Findings:**

* Interface: `enp0s3`

* Local IP: `10.0.2.15`

* Gateway: `10.0.2.2`

📸 *(See screenshots/system\_info/)*

---

## **🌐 2\. Connectivity & DNS Testing**

**Commands Used:**

`ping -c 4 8.8.8.8`  
`traceroute google.com`  
`dig openai.com +short`  
`ss -tuln`

**Results:**

* Verified internet connectivity

* Observed routing paths

* DNS resolution successful

* Listed open ports on system

📸 *(See screenshots/connectivity/)*

---

## **🔍 3\. Remote Host & Security Analysis**

**Commands Used:**

`nmap -Pn 10.0.2.2`  
`whois example.com`  
`nslookup example.com`  
`curl -I http://example.com`  
`ss -tunlp`  
`sudo ufw status verbose`  
`last`  
`sudo journalctl -u ssh`

**Results:**

* Remote scan of gateway device

* Resolved domain ownership and DNS info

* Observed firewall rules, listening services, and user login history

📸 *(See screenshots/security/)*

