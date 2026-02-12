# Active Directory Security Hardening & Attack Analysis

- Overview -
This project documents Active Directory (AD) security fundamentals, common attack techniques, log analysis strategies, and hardening recommendations from a Blue Team perspective.
The objective is to understand how attackers exploit AD environments and how defenders can detect and mitigate these threats effectively.

1. Active Directory Architecture Overview
Active Directory is a centralized identity and access management system used in Windows domain environments.

Key components:
Domain Controller (DC): Responsible for authentication and directory services.
LDAP: Protocol used for directory queries.
Kerberos: Default authentication protocol in modern AD environments.
NTLM: Legacy authentication protocol still present in some environments.
Group Policy Objects (GPO): Used to enforce security configurations across domain-joined machines.
Understanding these components is essential for both attack and defense strategies.

2. Authentication Process (Kerberos Overview)

When a user logs in:
The user requests authentication from the Domain Controller.
The DC issues a Ticket Granting Ticket (TGT).
The TGT is used to request service tickets.
Service tickets allow access to domain resources.
Security risks arise when attackers:
Steal tickets
Extract password hashes
Abuse service accounts

3. Common Active Directory Attacks
3.1 Brute Force
Repeated authentication attempts to guess credentials.

Detection:
Multiple failed login attempts (Event ID 4625)

Mitigation:
Account lockout policies
Strong password policies

3.2 Pass-the-Hash
Attackers reuse NTLM password hashes to authenticate without knowing the plaintext password.

Detection:
Suspicious authentication patterns
Logon type anomalies

Mitigation:
Disable NTLM where possible
Credential Guard
Least privilege enforcement

3.3 Kerberoasting
Attackers request service tickets for service accounts and attempt offline password cracking.

Detection:
High volume of TGS requests (Event ID 4769)
Requests targeting high-privilege service accounts

Mitigation:
Strong passwords for service accounts
Use of Managed Service Accounts

3.4 Privilege Escalation
Gaining elevated permissions through misconfiguration or credential abuse.

Detection:
Event ID 4672 (Special privileges assigned)
Changes to privileged groups (Event ID 4728, 4732)

Mitigation:
Monitor privileged groups
Apply least privilege principle
Regular auditing

4. Log Analysis & Monitoring Strategy

Important Event IDs:
4624 – Successful logon
4625 – Failed logon
4672 – Special privileges assigned
4728 – Member added to security-enabled global group
4732 – Member added to local group
4768 – Kerberos authentication ticket requested
4769 – Service ticket requested

Blue Team monitoring strategy:
Alert on multiple failed logins from the same IP
Monitor additions to Domain Admins group
Detect abnormal login times for privileged accounts
Track high volume of Kerberos ticket requests

5. Hardening Recommendations
Enforce strong password policies
Enable account lockout policies
Implement MFA for privileged accounts
Apply Least Privilege Principle
Regularly audit privileged groups
Disable NTLM where possible
Keep systems updated and patched

6. Blue Team Perspective
From a defensive standpoint, Active Directory is a high-value target. Continuous monitoring, log correlation, and strict privilege management are essential to reduce attack surface and improve detection capabilities.
