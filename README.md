# moveit-2023-cl0p-analysis

# MOVEit 2023 Exploitation (Cl0p) – Threat Intelligence Analysis

## Overview

This project analyzes the large-scale exploitation of the MOVEit Transfer vulnerability (CVE-2023-34362) by the Cl0p (TA505) ransomware group in 2023.

The attack leveraged a zero-day SQL injection vulnerability to enable unauthorized access and mass data exfiltration across thousands of organizations globally.

## Objectives

* Analyze the exploitation chain used in the MOVEit attack
* Map adversary behavior to MITRE ATT&CK
* Understand TA505 tactics and historical patterns
* Identify detection and mitigation opportunities

## Key Findings

* The attack exploited a zero-day SQL injection vulnerability in MOVEit Transfer
* Cl0p deployed the **LEMURLOOT webshell** to maintain access and exfiltrate data
* The campaign focused on **data theft and extortion**, not ransomware deployment
* File transfer systems remain high-value targets due to sensitive data concentration
* The attack followed a structured lifecycle aligned with the Cyber Kill Chain

## Attack Summary

The attack lifecycle included:

1. Reconnaissance of exposed MOVEit servers
2. Exploitation via SQL injection
3. Deployment of LEMURLOOT webshell
4. Persistence and database access
5. Data exfiltration over HTTP channels

## MITRE ATT&CK Mapping (Sample)

| Tactic         | Technique | Description                       |
| -------------- | --------- | --------------------------------- |
| Initial Access | T1190     | Exploit Public-Facing Application |
| Execution      | T1202     | Indirect Command Execution        |
| Persistence    | T1053     | Scheduled Task                    |
| Exfiltration   | T1041     | Exfiltration Over C2 Channel      |

## Impact

* Over **2,600 organizations** and **67 million individuals** affected
* Sectors impacted: healthcare, finance, education, government
* Demonstrates risk of **supply chain and third-party software vulnerabilities**

## Detection Opportunities

* Monitor abnormal SQL queries to MOVEit endpoints
* Detect unexpected file creation in web directories (.aspx files)
* Identify unusual outbound data transfers
* Analyze IIS logs for suspicious requests

## Recommendations

* Apply security patches immediately
* Restrict external access to file transfer services
* Implement network monitoring and logging
* Conduct vendor risk assessments for third-party software

## Skills Demonstrated

* Threat intelligence analysis
* Intrusion analysis and attack reconstruction
* MITRE ATT&CK mapping
* Threat actor profiling (TA505 / Cl0p)
* Security reporting and advisory writing

## Full Report

[View full academic report](./report/full_report.pdf)
