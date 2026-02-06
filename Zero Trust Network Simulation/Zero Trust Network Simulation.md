# **Zero Trust Network Simulation (Identity-Based Access)**

## **Project Overview**

Brief summary of the project’s purpose and scope.

* Simulated an enterprise **Zero Trust network architecture**

* Enforced **identity-based access controls**

* Implemented **default-deny network segmentation**

* Integrated **Active Directory authentication** with pfSense

* Designed **VPN-based secure access** to protected internal resources

**Core Principle:**

*Never trust the network. Always verify identity.*

## **Project Objectives**

Clearly list what the project aimed to achieve.

* Enforce identity-based access rather than network trust

* Segment internal networks with strict firewall rules

* Prevent lateral movement by default

* Require VPN authentication to access protected applications

* Validate controls using attacker simulation and logging

## **Lab Environment & Technology Stack**

### **Hypervisor**

* VirtualBox

### **Security & Network**

* pfSense CE 2.7.2 (Firewall, Routing, VPN)

* OpenVPN (Remote Access VPN)

* Suricata IDS (Planned / Optional)

### **Identity & Systems**

* Windows Server 2019 (Active Directory, DNS)

* Windows 10 / 11 (Domain-joined workstations)

* Ubuntu Server (Protected internal application)

* Kali Linux (Attack simulation)

## **🌐 Network Architecture**

### **Network Segmentation**

| Network | Subnet | Purpose |
| ----- | ----- | ----- |
| WAN | 10.0.2.0/24 | Internet access |
| Corp\_LAN | 10.0.10.0/24 | Trusted internal users |
| App\_NET | 10.0.20.0/24 | Protected application network |
| Guest\_NET | 10.0.30.0/24 | Untrusted / attacker network |

### **VirtualBox Networking**

* WAN → NAT

* Corp\_LAN → Internal Network

* App\_NET → Internal Network

* Guest\_NET → Internal Network

## **Firewall & Routing Design (pfSense)**

### **Interface Configuration**

* WAN: DHCP (10.0.2.15)

* Corp\_LAN: 10.0.10.1/24

* App\_NET: 10.0.20.1/24

* Guest\_NET: 10.0.30.1/24

### **Firewall Policy Model**

* Default deny on all internal interfaces

* Explicit allow rules only where required

* No lateral access between internal networks

* VPN required for App\_NET access

**Identity & Access Management (IAM)**

### **Active Directory Configuration**

* Domain: `corp.local`

* Domain Controller: Windows Server 2019

* DNS integrated with AD

### **Users & Groups**

| Group | Purpose |
| ----- | ----- |
| ZT-Employees | Standard VPN and app access |
| ZT-Admins | Administrative access |
| ZT-Denied | Explicit deny group |

### **LDAP Integration**

* pfSense authenticated users via Active Directory

* Successful LDAP authentication confirmed via pfSense GUI

## **Secure Remote Access Design (OpenVPN)**

### **Intended Access Flow**

1. User authenticates using AD credentials

2. VPN tunnel is established

3. Firewall rules allow access only to App\_NET

4. All other internal access remains denied

### **OpenVPN Server Configuration**

* Protocol: UDP IPv4

* Port: 1194

* Tunnel Network: 10.8.0.0/24

* Authentication: LDAP (Active Directory)

* Topology: Subnet

* Split tunneling enforced

## **Security Validation & Testing**

### **Expected Zero Trust Behavior**

| Test | Result |
| ----- | ----- |
| Guest\_NET → Corp\_LAN | ❌ Blocked |
| Guest\_NET → App\_NET | ❌ Blocked |
| Corp\_LAN → App\_NET (No VPN) | ❌ Blocked |
| VPN → App\_NET (Authenticated) | ✅ Intended |
| Lateral movement | ❌ Blocked |

### **Attack Simulation**

* Kali Linux used for:

  * `nmap` scans

  * Network reconnaissance

  * Connectivity testing

* Firewall logs verified blocked traffic

## **Troubleshooting & Challenges Encountered**

### **VPN Connectivity Issues**

* OpenVPN tunnel initialized but client connectivity failed

* Interface routing conflicts during reconfiguration

* Interface IP assignment errors after firewall reloads

### **WireGuard Attempt (Abandoned)**

* Kernel module (`if_wg`) failed to load on pfSense 2.7.2

* GUI key generation issues

* Switched to OpenVPN due to stability and support

### **Key Takeaway**

Real-world security environments involve complex dependencies where troubleshooting, documentation, and recovery are critical skills.

## **Monitoring & Logging**

* Firewall logging enabled on deny rules

* OpenVPN service logs reviewed

* Planned IDS integration using Suricata

* Logs intended for detection and audit validation

**Documentation & Evidence**

Included / Intended artifacts:

* Network design diagrams

* Firewall rule matrix

* LDAP authentication validation

* OpenVPN configuration (redacted)

* Firewall and VPN logs

* Screenshots of testing and failures

## **Lessons Learned**

* Zero Trust enforcement requires **tight coordination** between routing, firewall rules, identity systems, and VPNs

* VPN failures often stem from **interface misalignment**, not authentication

* Troubleshooting is a **core security skill**, not a failure

* Documenting intended outcomes is valuable when implementation hits blockers

## **Future Improvements**

* Rebuild VPN stack from a clean firewall snapshot

* Migrate to hardware firewall or alternative hypervisor

* Implement MFA for VPN authentication

* Centralize logs using SIEM (Splunk / ELK)

* Fully deploy Suricata IDS alerts

## **Skills Demonstrated**

* Zero Trust network design

* Firewall rule architecture (pfSense)

* Active Directory & LDAP integration

* Secure remote access planning

* Network segmentation and isolation

* Troubleshooting complex security systems

* Technical documentation for security projects

## **Appendix**

* Intended Network Diagram

* Firewall Rule Matrix

* AD User & Group Mapping

* Redacted OpenVPN Configuration

* Planned Detection Rules

