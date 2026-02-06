\# Windows Endpoint SOC Simulation using ELK & Sysmon

\#\# Overview  
This project demonstrates a mini Security Operations Center (SOC) simulation using Windows endpoints, Sysmon, Winlogbeat, and the ELK Stack. It collects and visualizes endpoint security telemetry, allowing SOC analysts to monitor processes, registry changes, file creation, PowerShell execution, Windows Defender alerts, and lateral movement.

\#\# Lab Environment  
\- \*\*Windows 10 Workstation:\*\* Endpoint with Defender    
\- \*\*Windows Server 2019:\*\* Attacker simulation    
\- \*\*Ubuntu ELK Server:\*\* Elasticsearch \+ Kibana    
\- \*\*Winlogbeat:\*\* Windows log forwarder    
\- \*\*Sysmon:\*\* Advanced system monitoring

\#\# Dashboards  
1\. \*\*Process & Registry Activity:\*\* Tracks process creation and registry modifications    
2\. \*\*File Creation Monitoring:\*\* Monitors new files created on endpoints    
3\. \*\*PowerShell Activity:\*\* Monitors script executions (Event ID 4104\)    
4\. \*\*Windows Defender Alerts:\*\* Tracks malware and operational events    
5\. \*\*Lateral Movement & Remote Activity:\*\* Monitors service creation and WMI execution

\#\# Key Observations  
\- Successful integration of Sysmon \+ Winlogbeat with ELK    
\- Dashboards provide actionable SOC-style visibility    
\- Encoded PowerShell commands and Defender test alerts may require policy adjustments    
\- Alerts are not configured (requires Kibana encryption key)

\#\# Next Steps  
\- Enable Kibana alerting    
\- Normalize log fields for improved querying    
\- Test additional threat scenarios (Atomic Red Team, ATT\&CK)    
\- Add Sigma rules for automated detections    
\- Expand lab with Linux endpoints

\#\# Author  
Chontele Coleman	    
11/12/2025

