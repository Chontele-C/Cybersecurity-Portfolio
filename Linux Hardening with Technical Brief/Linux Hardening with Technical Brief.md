\# Baker Street Corporation Linux Server Hardening Project

\#\# Overview  
This project details the security hardening and auditing performed on the Baker Street Corporation's Linux server (\`Hostname: Baker\_Street\_Linux\_Server\`), running Ubuntu 22.04.5 LTS (Jammy Jellyfish). The server contains sensitive and confidential data requiring robust protection against unauthorized access and security breaches.

\---

\#\# System Information

\- \*\*Hostname:\*\* Baker\_Street\_Linux\_Server    
\- \*\*OS Version:\*\* Ubuntu 22.04.5 LTS (Jammy Jellyfish)    
\- \*\*Memory:\*\* 15 GiB total (1.4 GiB used, 7.3 GiB free, 6.7 GiB buffered/cache)    
\- \*\*Swap:\*\* Disabled (0B)    
\- \*\*Uptime:\*\* 27 minutes (at time of audit)  

\---

\#\# Project Summary

Over a three-day period, the system was audited, hardened, and configured to follow best security practices, focusing on the principle of least privilege (PoLP), system integrity, and availability.

\#\#\# Day 1: User and Group Auditing, Password & Sudo Policies, File Permissions

\- Removed all terminated employees’ user accounts and home directories.  
\- Locked user accounts for staff on temporary leave.  
\- Verified and unlocked accounts of currently employed staff.  
\- Created a new group \`research\`, migrated users from the disbanded \`marketing\` group, and removed the \`marketing\` group.  
\- Enforced enhanced password policies requiring:  
  \- Minimum length of 8 characters    
  \- At least one uppercase letter    
  \- At least one special character    
  \- Two retry attempts for password entry    
\- Configured sudo privileges:  
  \- \`sherlock\` granted full sudo access    
  \- \`watson\` and \`mycroft\` granted sudo access only for \`/var/log/logcleanup.sh\`    
  \- Users in \`research\` group granted sudo access only for \`/tmp/scripts/research\_script.sh\`    
\- Removed world (other) permissions on user files and directories in \`/home\`.  
\- Located and removed hidden files containing stored passwords.

\#\#\# Day 2: Package & Service Hardening, SSH Security, Logging Configuration

\- Updated all installed packages and removed insecure packages (\`telnet\`, \`rsh-client\`).  
\- Installed security tools: \`ufw\` (firewall), \`lynis\` (security audit), and \`tripwire\` (intrusion detection).  
\- Disabled unnecessary services: stopped, disabled, and removed \`mysql\` and \`samba\`.  
\- Hardened SSH configuration:  
  \- Disabled empty passwords login    
  \- Disabled root login    
  \- Allowed only port 22    
  \- Enforced Protocol 2    
\- Configured persistent logging and log rotation:  
  \- Logs stored persistently with a max usage of 300MB    
  \- Log rotation changed from weekly to daily, keeping 7 days of logs  

\#\#\# Day 3: Automation & Scheduling

\- Created two scripts (\`hardening\_script1.sh\` and \`hardening\_script2.sh\`) automating Day 1 and Day 2 tasks.  
\- Scheduled scripts with cron:  
  \- \`hardening\_script1.sh\` runs monthly on the 1st at midnight    
  \- \`hardening\_script2.sh\` runs weekly every Monday at midnight  

\---

\#\# Key Commands & Configurations

\#\#\# User Management  
\`\`\`bash  
deluser \--remove-home \<terminated\_staff\>  
usermod \-L \<temp\_leave\_staff\>  
passwd \-S \<username\>  
sudo passwd \<username\>  
addgroup research  
delgroup marketing  
Password Policy (in /etc/pam.d/common-password)  
ruby  
Copy  
Edit  
password requisite pam\_pwquality.so minlen=8 ocredit=-1 retry=2 ucredit=-1  
Sudoers File Edits (sudo visudo)  
pgsql  
Copy  
Edit  
sherlock ALL=(ALL:ALL) ALL  
watson ALL=(ALL) NOPASSWD: /var/log/logcleanup.sh  
mycroft ALL=(ALL) NOPASSWD: /var/log/logcleanup.sh  
%research ALL=(ALL) NOPASSWD: /tmp/scripts/research\_script.sh  
File Permissions  
bash  
Copy  
Edit  
find /home \-type f \-perm /o+rwx \-exec chmod o-rwx {} \+  
find /home \-type d \-perm /o+rwx \-exec chmod o-rwx {} \+  
find /home \-type f \-iname '\*engineering\*' \-exec chown :engineering {} \+ \-exec chmod 770 {} \+  
find /home \-type f \-iname '\*research\*' \-exec chown :research {} \+ \-exec chmod 770 {} \+  
find /home \-type f \-iname '\*finance\*' \-exec chown :finance {} \+ \-exec chmod 770 {} \+  
SSH Configuration (/etc/ssh/sshd\_config)  
nginx  
Copy  
Edit  
PermitEmptyPasswords no  
PermitRootLogin no  
Port 22  
Protocol 2  
Package Management  
bash  
Copy  
Edit  
sudo apt update  
sudo apt upgrade \-y  
sudo apt install \-y ufw lynis tripwire  
sudo apt remove \-y telnet rsh-client  
sudo apt autoremove \-y  
Service Management  
bash  
Copy  
Edit  
sudo service mysql stop  
sudo service samba stop  
sudo systemctl disable mysql  
sudo systemctl disable samba  
Logging Configuration  
/etc/systemd/journald.conf

ini  
Copy  
Edit  
Storage=persistent  
SystemMaxUse=300M  
/etc/logrotate.conf

mathematica  
Copy  
Edit  
Daily  
Rotate 7  
Cron Scheduling  
bash  
Copy  
Edit  
0 0 1 \* \* /hardening\_script1.sh  
0 0 \* \* 1 /hardening\_script2.sh  
Tools Used  
UFW \- Firewall management

Lynis \- Security auditing

Tripwire \- Intrusion detection (file integrity monitoring)

Conclusion  
The Baker Street Corporation Linux server was effectively hardened by applying the principle of least privilege, updating software packages, disabling unnecessary services, enhancing password policies, securing SSH access, and automating routine hardening tasks. These measures significantly reduce the server’s attack surface, improve confidentiality, integrity, and availability of sensitive data.

Recommendations:

Continue staff security awareness training focused on phishing and physical security.

Maintain regular system audits and patching cycles.

Develop and test incident response and contingency plans for cyberattack scenarios.

Contact  
Prepared by: Chontele Coleman  
The Baker Street Corporation (BSC)  
Security Analyst

Attachments  
Screenshots and logs of commands and configurations (refer to project documentation folder)

hardening\_script1.sh and hardening\_script2.sh automation scripts

End of Report  
