# **Linux Kiosk Troubleshooting & Remote Support Simulation**

## **Project Overview**

**This project simulates a Linux-based kiosk environment similar to automated kiosks. The goal was to intentionally introduce realistic failures, diagnose them using Linux commands, and implement both manual and scripted fixes. It also includes a remote support simulation via SSH to mirror real-world troubleshooting scenarios.**

**The project demonstrates:**

* **Log analysis and error diagnostics**

* **File permission and process troubleshooting**

* **Bash scripting for automation**

* **Network troubleshooting**

* **Remote system administration**

* **Documentation and operational workflow**

## **Environment Setup**

**All project files are organized in a dedicated directory:**

**`~/kiosk`**

**This keeps logs, configuration files, and scripts isolated and mirrors production organization.**

**Files included:**

* **`kiosk_calibration.log` – Simulated calibration logs**

* **`kiosk_scanner.log` – Simulated scanner/cutter logs**

* **`kiosk_db.txt` – Mock database with intentional permission issues**

* **`calibrate_kiosk.py` – Example calibration script**

## **Simulated Issues**

**To replicate real-world kiosk problems, the following were introduced:**

1. **Calibration Failures – Errors added to `kiosk_calibration.log`**

2. **Scanner/Cutter Malfunctions – “Cutter jam detected” added to `kiosk_scanner.log`**

3. **File Permission Errors – `chmod 000 kiosk_db.txt`**

4. **Stopped Services – `pkill -f calibrate_kiosk.py`**

5. **Network Problems –**

   * **Blocked outbound HTTP: `sudo iptables -A OUTPUT -p tcp --dport 80 -j REJECT`**

   * **Incorrect DNS: `echo "nameserver 1.2.3.4" | sudo tee /etc/resolv.conf`**

---

## **Diagnostics & Troubleshooting**

### **Logs**

**Check calibration and hardware logs:**

**`tail -f ~/kiosk/kiosk_calibration.log`**

**`grep ERROR ~/kiosk/kiosk_calibration.log`**

**`tail -f ~/kiosk/kiosk_scanner.log`**

**`grep "error\|jam" ~/kiosk/kiosk_scanner.log`**

### **File Permissions**

**Verify access and fix issues:**

**`ls -l ~/kiosk/kiosk_db.txt`**

**`chmod 644 kiosk_db.txt`**

### **Processes**

**Check and restart services:**

**`ps aux | grep calibrate_kiosk.py`**

**`nohup python3 ~/kiosk/calibrate_kiosk.py &`**

### **Network**

**Check connectivity and DNS:**

**`ping 8.8.8.8`**

**`curl http://example.com`**

**`cat /etc/resolv.conf`**

### **System Resources**

**`df -h`**

**`free -h`**

**`top`**

## **Scripted Fixes**

### **Restart Calibration Script**

**`chmod +x ~/kiosk/calibrate_kiosk.py`**

**`pkill -f calibrate_kiosk.py`**

**`nohup python3 ~/kiosk/calibrate_kiosk.py &`**

**`echo "Calibration script restarted and permissions corrected."`**

### **Reset Scanner/Cutter Logs**

**`echo "Cutter cleared" > ~/kiosk/kiosk_scanner.log`**

**`echo "Scanner reset" >> ~/kiosk/kiosk_scanner.log`**

**`echo "Scanner and cutter logs cleared."`**

### **Network Recovery**

**`sudo iptables -F`**

**`echo "nameserver 8.8.8.8" | sudo tee /etc/resolv.conf`**

**`echo "Network issues cleared."`**

**Note: Scripts were executed via Bash rather than as standalone executables. The shebang (`#!/bin/bash`) is optional in this context because the commands were run directly from the terminal.**

## **Remote Support Simulation (SSH)**

**SSH was used to simulate real-world troubleshooting:**

**`ssh user@<vm-ip>`**

**Remote tasks included:**

* **Navigating to the kiosk directory**

* **Checking logs**

* **Verifying services**

* **Testing network connectivity**

* **Executing scripted fixes**

**This demonstrates how remote support can be performed without physical access.**

---

## **Optional Enhancements**

* **Cron Job Automation: Automatically restart calibration script every 30 minutes:**

**`crontab -e`**

**`# add line:`**

**`*/30 * * * * nohup python3 ~/kiosk/calibrate_kiosk.py &`**

* **Error Tracking: Future enhancement could include aggregating log errors via Python into a report.**

* **Random Failure Simulation: Additional logs or network issues can be triggered to practice advanced troubleshooting.**

## 

## **Lessons Learned**

* **Troubleshooting is most effective when done step-by-step and one issue at a time.**

* **Log analysis and pattern recognition are key to quickly identifying root causes.**

* **Permission and process checks are common sources of failures in Linux environments.**

* **`nohup` is a practical choice for temporary service recovery during troubleshooting; `systemd` is better for long-term deployment.**

* **Remote administration requires both technical knowledge and careful documentation to replicate field workflows.**

## **Skills Demonstrated**

* **Linux command line and shell scripting**

* **Log file analysis and grep/tail usage**

* **File and directory permissions management**

* **Process management and service troubleshooting**

* **Network diagnostics and recovery**

* **Remote system administration via SSH**

* **Documentation for internal knowledge bases**

   

     

 

 


 

