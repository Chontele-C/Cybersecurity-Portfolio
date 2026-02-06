\# AWS IAM Misconfiguration & Least-Privilege Hardening Lab

\#\# Overview  
This project demonstrates the identification and remediation of common AWS Identity and Access Management (IAM) misconfigurations that can lead to full cloud account compromise. The lab intentionally begins with an insecure administrative configuration, analyzes the associated risks, and applies least-privilege access controls, MFA enforcement, and centralized logging using AWS CloudTrail.

The objective of this project is to showcase practical cloud security decision-making, access control hardening, and detection validation using AWS Free Tier resources.

\---

\#\# Objectives  
\- Identify a real-world IAM misconfiguration involving excessive privileges  
\- Assess the security risks of over-permissioned IAM users  
\- Implement least-privilege access using group-based IAM policies  
\- Enforce multi-factor authentication (MFA)  
\- Enable and validate logging and detection using AWS CloudTrail  
\- Demonstrate professional scoping and security documentation practices

\---

\#\# Environment  
\- AWS Free Tier account  
\- AWS IAM (Users, Groups, Policies)  
\- AWS CloudTrail (Management Events)  
\- Optional EC2 (t2.micro) for access validation  
\- Local VirtualBox lab used only for AWS console access (no hybrid integration)

\---

\#\# Threat Model Summary  
A single IAM user with unrestricted administrative privileges represents a critical risk. If credentials are compromised, an attacker could:  
\- Create or modify IAM users and policies  
\- Disable logging to evade detection  
\- Delete or manipulate cloud resources  
\- Establish long-term persistence

This lab focuses on reducing that risk through least privilege, MFA, and logging.

\---

\#\# Initial Insecure Configuration  
An IAM user (\`legacy-admin\`) was intentionally created with the following characteristics:  
\- Directly attached \`AdministratorAccess\` policy  
\- AWS Management Console access  
\- No MFA enabled

This configuration violates the principle of least privilege and introduces a single point of failure for the entire AWS account.

\*\*Figure 1:\*\* IAM user with directly attached AdministratorAccess policy (misconfiguration)

\---

\#\# Detection Enablement  
AWS CloudTrail was configured to provide centralized logging and audit visibility:  
\- Multi-region trail enabled  
\- Management events (read and write) logged  
\- IAM and EC2 activity recorded for detection and review

CloudTrail ensures that administrative actions are logged and available for incident response and security audits.

\*\*Figure 2:\*\* CloudTrail configured to log management events across regions

\---

\#\# Remediation & Hardening

\#\#\# IAM Group Design  
To enforce least privilege and role-based access control, the following IAM groups were created:

\- \*\*IT-Support\*\*  
  \- Read-only access to EC2, S3, and CloudWatch  
\- \*\*Security-ReadOnly\*\*  
  \- AWS-managed \`SecurityAudit\` policy

No direct policies were attached to users.

\#\#\# Hardened User Configuration  
A new IAM user (\`it-support-user\`) was created with:  
\- Permissions inherited exclusively through group membership  
\- MFA enabled  
\- No administrative or write permissions

This design reduces attack surface and prevents privilege creep.

\*\*Figure 3:\*\* Role-based IAM group permissions enforcing least privilege    
\*\*Figure 4:\*\* MFA enabled for non-root IAM user

\---

\#\# Validation & Testing  
Access controls were validated by logging in as \`it-support-user\` and attempting unauthorized actions:

\- EC2 instance creation — \*\*Denied\*\*  
\- IAM user or policy modifications — \*\*Denied\*\*  
\- Logging configuration changes — \*\*Denied\*\*

AWS CloudTrail recorded these attempts as \`AccessDenied\` events, confirming that both preventive and detective controls were functioning correctly.

Once EC2 write permissions were confirmed to be denied, additional destructive testing (such as stopping or terminating instances) was considered redundant and out of scope.

\*\*Figure 5:\*\* CloudTrail logs showing \`AccessDenied\` events for unauthorized actions

\---

\#\# Scope & Limitations  
This lab focuses specifically on IAM misconfigurations, privilege management, and logging validation. Network security, application security, and data exposure scenarios were intentionally excluded to maintain a focused IAM security assessment.

\---

\#\# Future Enhancements  
The following enhancements were identified but not implemented to preserve scope clarity:  
\- S3 public exposure misconfiguration and remediation  
\- Multi-service IAM policy testing (EC2, S3, Lambda)  
\- Automated detection using AWS Config or Security Hub

These extensions demonstrate awareness of broader cloud security risks and phased assessment methodologies.

\---

\#\# Skills Demonstrated  
\- AWS IAM administration  
\- Least-privilege access design  
\- Cloud security threat modeling  
\- Logging, detection, and audit validation  
\- Security risk assessment and remediation  
\- Professional security documentation

\---

\#\# Conclusion  
This project demonstrates how common IAM misconfigurations can expose an AWS environment to significant risk and how structured remediation, MFA enforcement, and logging can effectively reduce the attack surface. The lab mirrors real-world cloud security assessments by emphasizing risk-based decision-making, scoped validation, and evidence-driven controls rather than exhaustive but redundant testing.

