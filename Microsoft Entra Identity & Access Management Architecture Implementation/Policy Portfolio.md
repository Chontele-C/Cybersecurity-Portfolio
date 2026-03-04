**\# Conditional Access Policy Portfolio**

This document outlines the Conditional Access policies designed for the DebRelSa Services IAM architecture.

Due to the lab environment operating under Microsoft Entra ID Free licensing, Conditional Access policies cannot be enforced. However, the following policies represent the intended production security architecture using Microsoft Entra ID P1/P2 capabilities.

These policies follow Zero Trust principles by enforcing strong authentication, reducing legacy protocol risk, and protecting privileged identities.

**| Policy | Scope | Control | Risk Mitigated |**  
|------|------|------|------|  
| Block Legacy Authentication | All Users | Block Legacy Protocols | Credential Replay |  
| Require MFA for Admins | GRP-CA-Admins | MFA | Privileged Account Compromise |  
| Require MFA for Contractors | GRP-CA-Contractors | MFA | External Identity Risk |

**\#\# Policy 1 — Block Legacy Authentication**

\*\*Scope:\*\*    
All workforce identities except emergency break-glass accounts.

\*\*Control:\*\*    
Block authentication attempts using legacy protocols such as POP, IMAP, SMTP AUTH, and other non-modern authentication mechanisms.

\*\*Threat Mitigated:\*\*    
Legacy authentication protocols bypass modern authentication protections such as MFA and Conditional Access evaluation. Attackers frequently exploit these protocols for credential replay attacks.

\*\*Security Rationale:\*\*    
Blocking legacy authentication forces all users to authenticate using modern authentication methods that support MFA and policy evaluation.

\*\*Licensing Requirement:\*\*    
Microsoft Entra ID P1

**\#\# Policy 2 — Require Multi-Factor Authentication for Administrators**

\*\*Scope:\*\*    
Administrative identities contained within GRP-CA-Admins.

\*\*Control:\*\*    
Require Multi-Factor Authentication (MFA) for all administrative sign-ins.

\*\*Threat Mitigated:\*\*    
Privileged accounts are high-value targets for attackers. Requiring MFA significantly reduces the likelihood of successful credential compromise.

\*\*Security Rationale:\*\*    
Administrative identities have elevated privileges and therefore require stronger authentication controls. Enforcing MFA aligns with Microsoft Zero Trust recommendations for protecting privileged roles.

\*\*Licensing Requirement:\*\*    
Microsoft Entra ID P1

**\#\# Policy 3 — Require MFA for Contractors**

\*\*Scope:\*\*    
Users within GRP-CA-Contractors.

\*\*Control:\*\*    
Require Multi-Factor Authentication during sign-in.

\*\*Threat Mitigated:\*\*    
Contractor identities often originate from external networks and unmanaged devices, increasing the risk of credential compromise.

\*\*Security Rationale:\*\*    
Requiring MFA ensures stronger identity verification for non-permanent workforce identities and reduces external identity risk.

\*\*Licensing Requirement:\*\*    
Microsoft Entra ID P1

**\#\# Zero Trust Alignment**

The Conditional Access policies in this portfolio support the Zero Trust security model by enforcing strong authentication, protecting privileged identities, and limiting authentication pathways that bypass modern security controls.

Together these policies reduce the risk of credential theft, unauthorized privilege escalation, and external identity compromise.