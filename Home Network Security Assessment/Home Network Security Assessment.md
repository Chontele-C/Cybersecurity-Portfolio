\# Home Network Security Assessment 

\#\# Author  
\- Chontele Coleman

\#\# Date  
\- December 2025

\#\# Project Type  
\- Defensive Security  
\- Network Assessment  
\- Home Lab

\#\# Tools Used  
\- Nmap  
\- arp-scan  
\- Kali Linux  
\- ISP Router Admin Interface

\---

\#\# Project Overview

This project documents a comprehensive home network security assessment focused on:

\- Establishing a network baseline  
\- Inventorying all connected devices  
\- Identifying open ports and services  
\- Validating router and wireless security controls  
\- Documenting real-world limitations of ISP-managed hardware

The assessment uses non-intrusive, defensive techniques and mirrors tasks commonly performed in SOC, IT, and GRC roles.

\---

\#\# Objectives

\- Discover all active devices on the local network  
\- Document IP addresses, MAC addresses, and manufacturers  
\- Identify exposed ports and running services  
\- Validate router perimeter security  
\- Assess wireless security configuration  
\- Establish a repeatable baseline for future comparison

\---

\#\# Network Environment

| Component | Details |  
|--------|--------|  
| Subnet | 192.168.1.0/24 |  
| Router | Spectrum (Model: SAX1V1K, ISP-managed) |  
| Testing Platform | Kali Linux VM |  
| Network Architecture | Flat LAN with Guest Wi-Fi isolation |

\---

\#\# Methodology

\#\#\# Host Discovery (ARP Scan)

ARP scanning was used to identify all Layer-2 reachable devices on the LAN.

\`\`\`bash  
sudo apt install \-y arp-scan  
sudo arp-scan \--localnet \--interface eth1 | tee report/arp\_scan.txt  
Purpose:

Identify live hosts

Map IP to MAC addresses

Detect devices not responding to ICMP

Network Mapping (Ping Sweep)  
A lightweight Nmap ping sweep was performed to confirm live hosts and hostnames.

bash  
Copy code  
sudo nmap \-sn 192.168.1.0/24 \-oN report/nmap\_ping\_sweep.txt  
Purpose:

Validate ARP scan results

Identify device naming patterns

Confirm host availability

Full Internal Network Scan  
A full SYN scan with service detection and OS fingerprinting was executed.

bash  
Copy code  
sudo nmap \-sS \-sV \-O 192.168.1.0/24 \-oA report/nmap\_full\_scan  
Findings:

Most ports on all hosts are closed or filtered

OS detection was limited due to lack of open ports

Timing and retransmission warnings indicate proper firewall behavior

This behavior reflects a secure and restrictive internal network posture.

Router Port and Service Scan (LAN Side)  
The router was scanned from the internal network.

bash  
Copy code  
sudo nmap \-p 1-65535 \-sV \-T4 \-Pn 192.168.1.1 \-oN report/router\_ports.txt  
Findings:

No unnecessary LAN-facing services exposed

Router management limited to internal access

UPnP Validation  
UPnP was checked to ensure no automatic port forwarding was active.

bash  
Copy code  
sudo nmap \-p 1900 \--script upnp-info 192.168.1.1 \-oN report/upnp\_check.txt  
Findings:

UPnP service closed

No UPnP discovery responses

Router Admin Panel Review  
The router’s admin interface was reviewed to document:

Connected devices

DHCP leases and IP assignments

Wireless security configuration

Guest network settings

Screenshots were captured and sanitized.

Local Neighbor Cache Validation  
Local ARP and neighbor caches were reviewed to confirm accuracy.

bash  
Copy code  
arp \-a  
ip neigh show  
Device Inventory  
All discovered devices were documented in:

text  
Copy code  
report/inventory.md  
Each entry includes:

Device name (generic)

IP address

MAC address (partially redacted)

Manufacturer (OUI lookup)

Open ports

Device role

Wireless Security Assessment  
Observed controls:

WPA2/WPA3-Personal enabled

SSID broadcast enabled

Guest Wi-Fi network enabled

Guest network isolated from LAN

WPS not exposed via user interface

Guest isolation was validated using ICMP reachability tests.

Validation and Attack Simulation (Non-Intrusive)  
Validation steps included:

External port scanning against the public IP address

Guest network isolation testing

UPnP and port forwarding verification

No exploitation or intrusive techniques were used.

Limitations  
ISP-managed router restricts:

VLAN creation

Firewall rule tuning

Traffic logging and syslog access

No dedicated Wi-Fi adapter for packet capture

Some devices were offline during scanning

These limitations were documented and considered during analysis.

Risk Summary  
Area	Risk Level	Notes  
External Exposure	Low	No WAN services exposed  
Internal Segmentation	Medium	Flat LAN architecture  
Wireless Security	Low	WPA2/WPA3 enforced  
Monitoring	Medium	Logging not accessible

Recommendations  
Upgrade to a user-managed router or firewall

Segment IoT and guest devices

Enable centralized logging and alerts

Re-run baseline scans quarterly

Evidence and Artifacts  
text  
Copy code  
report/  
├── arp\_scan.txt  
├── nmap\_ping\_sweep.txt  
├── nmap\_full\_scan.nmap  
├── router\_ports.txt  
├── upnp\_check.txt  
├── inventory.md

configs/  
└── dhcp\_leases.png  
All screenshots have sensitive information redacted.

Conclusion  
This project demonstrates practical network visibility, defensive security analysis, and professional documentation in a real-world constrained environment. It establishes a repeatable baseline and highlights common limitations of ISP-managed infrastructure.

Disclaimer  
This assessment was conducted on systems and networks owned by the author. No unauthorized scanning or exploitation was performed.

