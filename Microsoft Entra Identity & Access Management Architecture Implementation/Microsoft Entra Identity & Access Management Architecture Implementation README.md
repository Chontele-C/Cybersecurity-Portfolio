# **Microsoft Entra Identity & Access Management Architecture Implementation**

**Author:** Chontele Coleman  
**Environment:** Microsoft Entra ID (Free Tier)  
**Focus:** Identity Architecture, RBAC, Identity Lifecycle Governance, and Zero Trust Conditional Access Design

# **Project Overview**

This project demonstrates the design and implementation of a secure Identity and Access Management (IAM) architecture using Microsoft Entra. The objective was to simulate how identity systems are structured and governed in a real organizational environment while applying security best practices aligned with Zero Trust principles.

The project focuses on architecture design and governance rather than simple configuration tasks. Key identity management concepts implemented include role-based access control, identity lifecycle management, administrative tier separation, and Conditional Access policy design.

Because the tenant environment operates under Microsoft Entra ID Free licensing, some features such as Conditional Access enforcement and group-based role assignments were documented as architectural designs rather than implemented configurations.

# **Project Objectives**

The goals of this project were to:

• Design a scalable identity architecture within Microsoft Entra  
• Implement Role-Based Access Control (RBAC)  
• Separate privileged and non-privileged identities  
• Organize identities using security groups  
• Simulate identity lifecycle events (Joiner, Mover, Leaver)  
 • Demonstrate governance through audit logs  
 • Design Conditional Access policies aligned with Zero Trust security principles

# **Identity Architecture Design**

All workforce identities were managed within a centralized Microsoft Entra tenant. Access to resources, applications, and administrative capabilities was governed through identity roles, group organization, and monitoring through audit logs.

The architecture followed a structured identity model designed to reduce privilege exposure and improve access governance.

# **Administrative Tier Model**

A simplified administrative tier model was implemented to separate privileged accounts from operational and standard user identities.

### **Tier 0 — Privileged Administration**

Highly restricted accounts responsible for tenant-wide administration.

Example account:  
cc-admin

Responsibilities include:

• Global Administrator access  
• Tenant configuration  
• Identity governance oversight

### **Tier 1 — IT Operations**

Operational administrative accounts responsible for user support and identity management tasks.

Example accounts:  
helpdesk1  
itops1

Responsibilities include:

• User account management  
• Password resets  
• Identity troubleshooting

### **Tier 2 — Standard Users**

Regular workforce identities with no administrative privileges.

Example accounts:  
exec1  
contractor1  
cc-user

These identities operate with standard permissions and limited access to administrative functions.

# **Role-Based Access Control (RBAC)**

Role-Based Access Control was implemented to enforce the principle of least privilege.

Directory roles were assigned as follows:

Helpdesk Administrator → helpdesk1  
User Administrator → itops1  
Global Administrator → cc-admin

Due to the limitations of the Microsoft Entra ID Free environment, roles were assigned directly to users. In a licensed production environment, roles would be assigned through role-based security groups to support scalable identity governance.

# 

# **Identity Group Architecture**

Security groups were created to represent workforce populations and policy scopes.

### **Workforce Population Groups**

GRP-POP-Employees  
GRP-POP-Contractors

These groups categorize identities based on workforce type.

### **Conditional Access Scope Groups**

GRP-CA-Admins  
GRP-CA-Users  
GRP-CA-Contractors  
GRP-EXCLUDE-BreakGlass

These groups were designed to define how Conditional Access policies would be applied in a licensed production environment.

# **Enterprise Application Access Model**

A simulated enterprise application called **Demo-SaaS-App** was created to demonstrate identity-based application access management.

Within the lab environment, application access was assigned directly to users due to licensing limitations.

### **Production Design Model**

Users → Application Access Groups → Enterprise Applications

This design supports scalable access provisioning, simplifies lifecycle management, and improves audit visibility.

# **Identity Lifecycle Management**

Identity lifecycle scenarios were simulated to demonstrate how organizations manage identity provisioning and deprovisioning.

### **Joiner Scenario**

A new user account was created to simulate employee onboarding.

Provisioning steps included:

• Creating the user identity  
• Assigning population groups  
• Granting required application access

This demonstrates how new users inherit permissions based on identity group membership.

### **Mover Scenario**

A role transition was simulated by changing administrative permissions.

Example:

helpdesk1 transitioned to IT operations responsibilities.

Role reassignment demonstrates how identity access can be adjusted as job responsibilities change.

### **Leaver Scenario**

An offboarding scenario was simulated for contractor1.

The offboarding workflow included:

• Disabling the user account (Account Enabled set to No)  
• Removing application access  
• Removing group memberships  
• Verifying actions through audit logs

This process demonstrates how organizations securely revoke access when identities leave the organization.

# **Governance and Auditability**

Identity governance was validated using Microsoft Entra audit logs.

Administrative activities recorded included:

• User account modifications  
• Role assignments  
• Group membership changes  
• Identity lifecycle events

Each audit log entry records:

• Actor (who performed the action)  
• Action (what was performed)  
• Target (which identity was affected)  
• Timestamp (when the event occurred)

These records provide accountability and traceability for identity administration actions.

# **Conditional Access Policy Design**

Conditional Access policies were designed as part of a Zero Trust identity architecture portfolio.

Because the environment operates under Microsoft Entra ID Free licensing, these policies were documented rather than enforced.

### **Policy 1 — Block Legacy Authentication**

Scope: All users except emergency break-glass accounts

Control:  
Block authentication attempts using legacy protocols.

Threat Mitigated:  
Credential replay attacks and authentication bypass risks.

Licensing Requirement:  
Microsoft Entra ID P1

### **Policy 2 — Require Multi-Factor Authentication for Administrators**

Scope:  
Administrative identities (GRP-CA-Admins)

Control:  
Require MFA during authentication.

Threat Mitigated:  
Privileged account compromise.

Licensing Requirement:  
Microsoft Entra ID P1

### **Policy 3 — Require MFA for Contractors**

Scope:  
GRP-CA-Contractors

Control:  
Require MFA during authentication.

Threat Mitigated:  
External identity compromise from unmanaged networks or devices.

Licensing Requirement:  
Microsoft Entra ID P1

# **Zero Trust Alignment**

The architecture aligns with Zero Trust identity security principles.

Key controls include:

• Separation of privileged and standard identities  
• Strong authentication design using MFA policies  
• Blocking insecure legacy authentication methods  
• Identity lifecycle governance  
• Continuous monitoring through audit logs

The architecture assumes that no identity is inherently trusted and requires verification through identity controls.

# **Environment Limitations**

The project environment used Microsoft Entra ID Free licensing, which restricts several advanced identity security capabilities.

Limitations included:

• Conditional Access enforcement  
• Group-based role assignment  
• Group-based application assignment  
• Privileged Identity Management (PIM)

These controls were documented as architectural designs rather than implemented configurations.

# **Skills Demonstrated**

Microsoft Entra Identity Administration  
Identity Architecture Design  
Role-Based Access Control (RBAC)  
Identity Lifecycle Governance  
Conditional Access Design  
Zero Trust Security Principles  
IAM Governance and Audit Monitoring

# 

# 

# **Project Outcome**

This project demonstrates how identity systems can be designed to support secure access management, governance, and lifecycle control using Microsoft Entra.

The architecture illustrates how organizations can structure identity governance processes to reduce risk, enforce least privilege, and support secure authentication practices aligned with modern Zero Trust security frameworks.

