\# DNS and SSL Remediation Case Study

\#\# Overview  
This project documents a real-world technical incident involving \*\*DNS conflicts, SSL certificate failures, and subdomain resolution\*\* caused by a hybrid hosting setup using \*\*Wix\*\* and \*\*Kartra\*\*.  

The root domain (\`exampledomain.com\`) was managed in Wix, while the primary website (\`www.exampledomain.com\`) was hosted on Kartra. This caused SSL issuance failures and “Connection Not Private” errors.  

A blog subdomain (\`blog.exampledomain.com\`) was created to separate services, stabilize DNS, and ensure proper SSL coverage.

\---

\#\# Objective  
\- Resolve SSL certificate errors for root and main domains    
\- Correct DNS misconfigurations    
\- Maintain functionality of the primary site hosted on Kartra    
\- Create a functional blog subdomain on Wix without interfering with the main site    
\- Document the troubleshooting and remediation process for educational purposes

\---

\#\# Platforms Involved  
\- \*\*Wix\*\* – DNS host and blog subdomain hosting    
\- \*\*Kartra\*\* – Website hosting and SSL issuance for the primary site

\---

\#\# Tools & Techniques  
\- \*\*OpenSSL\*\* – for SSL handshake analysis    
\- \*\*nslookup\*\* – for DNS resolution verification    
\- \*\*DNS Checker\*\* – to verify global DNS propagation    
\- \*\*SSL Labs Server Test\*\* – to evaluate SSL configuration    
\- \*\*SSL Checker\*\* – to confirm certificate validity    
\- WHOIS lookup – for nameserver verification    
\- Operating systems: Windows 10, Kali Linux  

\---

\#\# Findings  
\- Root domain (\`exampledomain.com\`) pointed to Wix, preventing SSL issuance    
\- Main site (\`www.exampledomain.com\`) pointed to Kartra via CNAME    
\- SSL conflicts prevented browsers from trusting either domain    
\- Wix low-tier plans restrict DNS editing, limiting ability to fix conflicts    
\- Kartra requires CNAME pointing and DNS control to issue SSL  

\---

\#\# Actions Taken  
1\. \*\*Blog Subdomain Creation\*\* – created \`blog.exampledomain.com\` on Wix    
   \- Required paid Wix plan to access DNS editor    
   \- Subdomain successfully issued a valid SSL certificate    
2\. \*\*Root Domain Considerations\*\* – determined root domain needed transfer to Kartra for permanent SSL fix    
3\. \*\*DNS & SSL Verification\*\* – confirmed propagation, validity, and resolution of conflicts  

\---

\#\# Lessons Learned  
\- Hybrid setups between Wix and Kartra can easily lead to DNS and SSL conflicts    
\- Low-tier or free plans may restrict DNS access and SSL issuance    
\- Subdomains are an effective solution to separate services and avoid platform limitations    
\- Thorough diagnostics (OpenSSL, nslookup, SSL Labs) are essential for identifying root causes  

\---

\#\# Limitations  
Due to \*\*client privacy and security considerations\*\*, screenshots of DNS records, SSL test results, and platform dashboards have not been included. Including these would reveal domain-specific information, IP addresses, and account details.  

All technical findings, remediation steps, and results are fully documented in the text, providing a complete overview of the incident and resolution. While screenshots would provide visual confirmation, omitting them ensures this repository is safe for public viewing.

\---

\#\# Conclusion  
The DNS and SSL issues were fully identified and remediated:

\- DNS integrity restored    
\- SSL certificates issued correctly    
\- Blog subdomain separated services to prevent conflicts    
\- Site is now stable, secure, and configured according to best practices  

This case study demonstrates real-world troubleshooting, platform limitations, and solutions for DNS/SSL conflicts in hybrid hosting environments.

