# **Azure Control Plane Monitoring & Insider Threat Detection**

## **Project Overview**

This project demonstrates how Azure control plane activity can be monitored, investigated, and mapped to governance and risk frameworks to detect insider threat behavior. The focus is on **identity lifecycle events, role-based access control (RBAC) changes, and audit visibility**, which are frequently exploited in real-world cloud security incidents.

The lab was intentionally built using **Azure Free Tier** to reflect realistic constraints while preserving strong security controls such as mandatory MFA. Rather than bypassing protections for the sake of simulation, the project highlights how effective controls deter low-effort or low-value attacker activity.

This project is designed for **IT Support, SOC Analyst, Cloud Security, and GRC-adjacent roles**.

---

## **Objectives**

* Validate default Azure control plane logging  
* Simulate insider-risk behavior without weakening tenant security  
* Analyze administrative actions from a SOC analyst perspective  
* Map technical findings to NIST and ISO security controls

---

## **Environment**

* **Cloud Platform:** Microsoft Azure (Free Tier)  
* **Identity Provider:** Microsoft Entra ID  
* **Logging Sources:** Azure Activity Log, Entra ID Audit Logs  
* **Security Posture:** Security Defaults enabled (mandatory MFA)

---

## **Step 1 — Baseline Logging Validation**

**Goal:** Understand what Azure logs by default in a new subscription.

**Actions:**

* Reviewed Azure Monitor → Activity Log  
* Identified default retention and event categories  
* Confirmed no baseline events are generated prior to administrative activity

**Key Insight:**  
Azure does not generate synthetic or baseline control-plane events. Logging begins only after management actions occur.

---

## **Step 2 — Simulated Insider Behavior**

**Goal:** Generate high-signal control-plane events associated with insider misuse.

**Actions:**

* Created a new Entra ID user (`temp.insider`)  
* Assigned elevated RBAC permissions at the subscription level  
* Removed permissions shortly after assignment  
* Preserved mandatory MFA enforcement

**Threats Simulated:**

* Unauthorized account provisioning  
* Privilege escalation  
* Short-lived elevated access

---

## **Step 3 — SOC Analyst Investigation**

**Goal:** Investigate generated events as a SOC analyst would during triage.

**Analysis Questions:**

* Who initiated the action?  
* What privilege level did they hold?  
* Was the behavior expected?  
* What indicators raise concern?

### **SOC Findings**

| Event | Risk | Detection Source | Recommended Control |
| ----- | ----- | ----- | ----- |
| User creation | Unauthorized access | Entra ID Audit Logs | Approval workflows |
| Role assignment | Privilege escalation | Azure Activity Log | Least privilege RBAC |
| Rapid role removal | Covering tracks | Azure Activity Log | Time-based alerts |
| MFA enforcement | Attack deterrence | Security Defaults | Maintain MFA |

---

## **Step 4 — GRC Control Mapping**

**Goal:** Translate technical findings into governance and compliance language.

### **NIST SP 800-53**

* **AC-2 (Account Management):** Account creation and privilege changes were auditable; approval workflows were not enforced.  
* **AU-2 (Audit Events):** Core administrative actions were logged with attribution; some tenant-level security changes lacked visibility.

### **ISO/IEC 27001**

* **Annex A.9 (Access Control):** RBAC and MFA effectively limited insider misuse; privileged access governance could be formalized.

**Assessment:** Controls were partially implemented with identifiable gaps and actionable recommendations.

---

## **Security Control Effectiveness**

Mandatory MFA significantly increased attacker friction. For a low-value test account, the requirement to enroll authentication factors acted as an effective deterrent. This aligns with real-world attacker behavior, where high-friction controls often cause attackers to abandon targets rather than escalate effort.

---

## **Key Takeaways**

* Azure control-plane actions are highly valuable for insider threat detection  
* IAM abuse is a primary insider risk vector in cloud environments  
* Strong default security controls reduce attacker ROI  
* Meaningful SOC and GRC analysis can be performed without bypassing protections

---

## **Skills Demonstrated**

* Azure control plane monitoring  
* Identity and access management analysis  
* Insider threat detection concepts  
* SOC-style log investigation  
* NIST and ISO control mapping  
* Security-first decision making

---

## **Notes**

This project intentionally respects free-tier and security-default limitations. No premium features or security bypasses were used.

---

*Author: Chontele Coleman*

