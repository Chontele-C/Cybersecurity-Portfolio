\# Organizational Risk Assessment & Heat Map Analysis

\#\# 🔍 Overview  
This project demonstrates a Governance, Risk, and Compliance (GRC) approach to identifying, analyzing, and visualizing organizational cybersecurity risks using a risk heat map. It follows a structured methodology using Likelihood × Impact scoring to evaluate and prioritize 14 risks.

\#\# 🎯 Objectives  
\- Identify and categorize common cybersecurity risks  
\- Calculate Risk Severity Scores (Probability × Impact)  
\- Visualize the risks in a heat map  
\- Categorize risks by severity level (Negligible to Critical)  
\- Propose mitigation recommendations

\#\# 📊 Risk Scoring Model  
\- \*\*Likelihood\*\*: Scale of 1 (Rare) to 5 (Almost Certain)  
\- \*\*Impact\*\*: Scale of 1 (Minimal) to 16 (Catastrophic)  
\- \*\*Risk Score\*\* \= Likelihood × Impact

\#\#\# Severity Classification:  
| Score Range | Risk Level   |  
|-------------|--------------|  
| 1–2         | Negligible   |  
| 3–8         | Minor        |  
| 10–16       | Moderate     |  
| 20–32       | High         |  
| 40–80       | Critical     |

\#\# 📈 Heat Map Summary

| Impact ↓ / Likelihood → | 1     | 2     | 3     | 4     | 5     |  
|-------------------------|-------|-------|-------|-------|-------|  
| 16                      |       |       | 48%   | 43%   |       |  
| 8                       |       |       | 14%   | 36%   |       |  
| 4                       |       | 7%    |       |       |       |  
| 2                       |       |       |       |       |       |  
| 1                       | 0%    |       |       |       |       |

\#\# 🧾 Risk Assessment Data Table

| ID  | Risk Description               | Likelihood (1–5) | Impact (1–16) | Risk Score | Notes |  
|-----|--------------------------------|------------------|---------------|------------|-------|  
| R1  | Data Breaches                 | 3                | 4             | 12         |       |  
| R2  | Ransomware                    | 4                | 16            | 64         |       |  
| R3  | Unauthorized Network Access   | 4                | 2             | 8          |       |  
| R4  | Single Point of Failure       | 3                | 16            | 48         |       |  
| R5  | No Content Filtering          | 3                | 16            | 48         |       |  
| R6  | Weak VPN                      | 3                | 16            | 48         |       |  
| R7  | Lateral Movement              | 3                | 8             | 24         |       |  
| R8  | Privilege Escalation          | 3                | 8             | 24         |       |  
| R9  | Outdated Devices              | 2                | 8             | 16         |       |  
| R10 | Stolen Cookies                | 4                | 16            | 64         |       |  
| R11 | Brute Force Attacks           | 3                | 8             | 24         |       |  
| R12 | Sensitive Data Exposed        | 4                | 16            | 64         |       |  
| R13 | Reflective XSS                | 3                | 8             | 24         |       |  
| R14 | Admin Tools Exposed to Public | 2                | 16            | 32         |       |

\---

\#\# 🛡️ Key Takeaways  
\- \*\*High and Critical Risks\*\* (Scores ≥ 20\) should be prioritized for mitigation.  
\- \*\*Ransomware\*\*, \*\*Sensitive Data Exposure\*\*, and \*\*Stolen Credentials\*\* were rated \*\*Critical\*\*.  
\- Recommended controls include endpoint detection, zero trust access, and patch management.

\#\# 📎 Files Included  
\- \`Risk\_Assessment\_Report.md\` — This write-up  
\- \`Risk\_Assessment\_Report.pdf\` — Formatted version  
\- \`risk\_assessment\_heat\_map.xlsx\` — Optional Excel visual

\---

\#\# ✅ GRC Domains Covered  
\- Risk Management  
\- Governance & Compliance Reporting  
\- Control Recommendations  
