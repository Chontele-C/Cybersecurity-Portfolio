\# Cybersecurity Lab Project Report  

\*\*Windows Event Collection & SOC Dashboard with Winlogbeat, Elasticsearch, and Kibana\*\*

—

	\#\# Project Summary

This project demonstrates the creation of a SOC-style monitoring environment using open-source tools. Windows event logs were collected from a Windows 10 workstation and a Windows Server Domain Controller with Winlogbeat, shipped to Elasticsearch, and visualized in Kibana. The resulting dashboards enable real-time detection of failed logins, process creation, and service manipulation events—core activities that security analysts investigate during incident response.

\---

\#\# 1\. Introduction

This project demonstrates how to build a SOC-style monitoring environment using open-source tools.  

Windows event logs were collected from a Windows 10 workstation and a Windows Server Domain Controller, shipped to Elasticsearch with Winlogbeat, and visualized in Kibana dashboards.


\*\*Goals of the lab:\*\*

\- Collect critical Windows Security events.

\- Validate end-to-end log flow from endpoints to Elasticsearch.

\- Build custom Kibana visualizations and dashboards for SOC-style analysis.

\*\*Tools & Systems:\*\*

\- \*\*Kali Linux VM\*\* – Elasticsearch 8.19.2 \+ Kibana.

\- \*\*Windows 10 VM\*\* – Endpoint log source.

\- \*\*Windows Server 2019 (Domain Controller)\*\* – Domain log source.

\- \*\*Winlogbeat 9.1.1\*\* – Windows log shipper.

\---

\#\# 2\. Lab Environment Setup

\#\#\# 2.1 Kali Linux VM

\- Installed \*\*Elasticsearch 8.19.2\*\* and \*\*Kibana\*\*.

\- Configured \`server.host: "0.0.0.0"\` for network access.

\- Verified Elasticsearch service:

sudo systemctl status elasticsearch

Confirmed cluster active:

curl \-k \-u elastic:\<password\> https://localhost:9200

Kibana accessible via:

http://192.168.56.110:5601

2.2 Windows VMs

Installed Winlogbeat 9.1.1 on both Windows 10 and Windows DC.

Configured to ship logs to Elasticsearch.

Example winlogbeat.yml configuration:

winlogbeat.event\_logs:

  \- name: Application

  \- name: Security

  \- name: System

  \- name: Setup

  \- name: ForwardedEvents

output.elasticsearch:

  hosts: \["https://192.168.56.110:9200"\]

  username: "elastic"

  password: "\<elastic\_password\>"

  ssl.verification\_mode: none

setup.kibana:

  host: "http://192.168.56.110:5601"

setup.dashboards.enabled: true

logging.level: info

logging.to\_files: true

logging.files:

  path: C:/ProgramData/winlogbeat/Logs

  name: winlogbeat

  keepfiles: 7

  permissions: 0644

Verified Winlogbeat running:

Get-Service winlogbeat

3\. Event Collection & Validation

3.1 Security Events Captured

✅ 4625 – Failed logon attempts

✅ 4624 – Successful logons

✅ 4688 – Process creation

⚠️ 7045 – Service creation (limited fields populated)

3.2 Validation

Used Kibana Discover to confirm logs ingestion.

Adjusted time range (last 36 hours) to ensure visibility.

Noted: many service creation events logged under SYSTEM or machine accounts.

4\. Visualization Setup

4.1 Saved Searches

Created saved searches for event codes: 4625, 4624, 4688, 7045\.

4.2 Visualizations

4625 Failed Logins → Bar chart over time.

4624 Successful Logins → Bar chart split by host.

4688 Process Creation → Vertical bar chart by host.

7045 Service Creation → Pie/Bar chart by host.

5\. Dashboard Design

5.1 Layout

Top Row – Authentication

Failed Logins (4625)

Successful Logins (4624)

Middle Row – Execution & Persistence

Process Creation (4688)

Service Creation (7045)

Bottom Row – Raw Data

Data table showing:

@timestamp

event.code

user.name

host.name

5.2 Workflow

Analysts can filter on event.code, host.name, or user.name.

Failed vs successful logins help detect brute force or suspicious access.

Process and service creation events highlight potential attacker persistence.

Raw data table provides quick access to underlying event logs.

6\. Challenges & Observations

Usernames: Logged as SYSTEM, ADMINISTRATOR, or machine accounts instead of test users.

7045 Service Creation: process.name and service.name fields did not populate.

Workaround: Visualizations still useful for event correlation and detection trends.

7\. Conclusion

Built a functional SOC-style dashboard with Elasticsearch, Kibana, and Winlogbeat.

Verified event log pipeline from Windows endpoints to dashboards.

Dashboard enables monitoring of failed logins, successful logins, process creation, and service creation.

8\. Future Improvements

Add Sysmon for richer event logging (process hashes, network activity).

Enable Advanced Audit Policies for more detailed event data.

Configure alerting (Kibana alerts or ElastAlert).

Expand lab with phishing or malware simulation for realistic SOC scenarios.

