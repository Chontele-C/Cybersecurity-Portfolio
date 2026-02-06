# **Monitoring & Analyzing Attacks in Splunk**

This project simulates the role of a Security Operations Center (SOC) analyst at **Virtual Space Industries (VSI)**, a company that develops virtual-reality software. VSI suspects cyberattacks from a competitor, **JobeCorp**, and has tasked us with using **Splunk** to detect, analyze, and report on suspicious activity from **Windows** and **Apache** server logs.

---

## **📊 Monitoring Environment**

* **Tools:** Splunk Enterprise  
* **Data Sources:**  
  * Windows Security Audit logs (CSV format)  
  * Apache HTTP server logs (Combined Log Format)

---

## **📁 Logs Analyzed**

### **🪟 Windows Logs**

* CSV export of Windows Security Audit events  
* Fields include:  
  * `_time`: Timestamp  
  * `host`: Hostname  
  * `signature_id`: Numeric event ID (e.g. 4624, 4726\)  
  * `signature`: Human-readable event description  
  * `severity`: Informational, High, etc.  
  * `status`: Success or Failure  
  * `user`: Account involved  
  * Additional context: process, IP address, etc.

### **🌐 Apache Logs**

* Combined Log Format  
* Fields include:  
  * `_time`: Timestamp  
  * `clientip`: Originating IP  
  * `http_method`: GET, POST, etc.  
  * `uri`: Requested URI  
  * `status`: HTTP response code  
  * `bytes`: Size of response  
  * `referrer`: Previous URL  
  * `user_agent`: Browser or bot ID

---

## **📈 Reports**

### **Windows Reports**

#### **✅ Signatures & Signature IDs**

Mapping Windows event IDs to human-readable activity for better alerting.

#### **🔥 Severity Levels (4764 events total)**

* Provides a breakdown by severity (Informational, High, etc.)  
* Visualized via pie chart & bar graph

#### **⛔ Success vs. Failure**

* Status-based analysis to identify anomalies in expected success rates

### **Apache Reports**

#### **📑 HTTP Methods Used**

* Trends in usage (GET vs POST)

#### **🌍 Top 10 Referer Domains**

* Identify suspicious referrer behavior

#### **📟 HTTP Status Codes**

* Highlighted spike in 404 (Not Found) indicates path fuzzing or probing

---

## **🚨 Alerts**

### **Windows Alerts**

#### **🔐 Failed Windows Activity**

* **Runs:** Hourly  
* **Threshold:** \>10 failures/hour  
* **Baseline:** \~5.9 failures/hour  
* **Action:** Email alert to `SOC@VSI-company.com`  
* **Justification:** Normal range is 4–10; threshold avoids false positives

#### **👤 Successful Logon Surge (Event ID: 4624\)**

* **Runs:** Hourly  
* **Threshold:** \>20 logons/hour  
* **Baseline:** \~10 logons/hour  
* **Justification:** 20 \= mean \+ 2σ; detects spikes like credential-stuffing

#### **🗑️ User Account Deletions (Event ID: 4726\)**

* **Runs:** Hourly  
* **Threshold:** \>3 deletions/hour  
* **Baseline:** \<1/hour  
* **Justification:** Uses 95th percentile to detect true anomalies

### **Apache Alerts**

#### **🌐 Activity Outside the U.S.**

* **Runs:** Hourly  
* **Threshold:** \>130/hour  
* **Baseline:** 40–90/hour  
* **Triggered:** Once, with 1,415 foreign events

#### **📤 HTTP POST Count**

* **Runs:** Hourly  
* **Threshold:** \>5 POST/hour  
* **Baseline:** 0–4/hour  
* **Triggered:** 1,296 POSTs at 8PM on 3/25/2020

---

## **🧪 Attack Findings**

### **Windows Summary**

* 2PM–3PM: 12 failed logons detected (\>10 threshold)  
* 11AM–12PM: 4 account deletions (\>3 threshold)  
* 3PM–4PM: 250 successful logons by `AdminUser1` (\>230 threshold)

These form a **recon → cleanup → access** attack pattern.

### **Apache Summary**

* Surge in `POST` requests indicates likely exploit attempt or file upload probe  
* Referrer domain `semicomplete.com` used in potential spoofing  
* Surge in `404 Not Found` suggests directory brute-forcing  
* Geographic spike in traffic from **Kiev, Ukraine**  
* URI focus shifted to `/VSI_Account_logon.php` (logon target)  
* Increased use of outdated `Mozilla/4.0` user-agent — common bot signature

---

## **🧠 Dashboards**

* **User Account Deletions:** Notable spike from 11AM–12PM  
* **Logon Surge:** AdminUser1 spike from 3PM–4PM  
* **Client GeoStats:** Increased activity from Eastern Europe (Kiev)  
* **URI Path:** `/VSI_Account_logon.php` now most accessed URI  
* **Top Countries:** Normalized traffic globally but elevated risk from Ukraine  
* **User Agent:** Surge in `Mozilla/4.0` — indicates automation or reconnaissance

---

## **🔐 Project Summary & Mitigations**

### **🧾 Summary**

* Windows: Account lockouts, password resets, mass logons  
* Apache: High POST/GET spikes, foreign access, outdated agents

### **🛡️ Recommendations**

1. **Geo-blocking:** Deny high-risk regions via firewall  
2. **Rate-limiting & MFA:** Mitigate brute-force attacks  
3. **Logon hardening:** Introduce lockout thresholds  
4. **Update detection:** Alert on outdated user agents

---

### **📌 Note**

All thresholds used `mean + 2σ` to maintain a balance between sensitivity and avoiding alert fatigue. Alerts only triggered on true anomalies.

