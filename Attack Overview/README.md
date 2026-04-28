## II. Attack Overview

The MOVEit Transfer exploitation campaign was a large-scale, financially motivated zero-day attack attributed to the Cl0p ransomware ecosystem (linked to TA505). The operation involved systematic exploitation of vulnerabilities in the MOVEit Transfer application to enable mass data exfiltration across multiple organizations.

Evidence from threat intelligence research indicates that Cl0p-associated actors were actively testing exploitation techniques targeting MOVEit Transfer as early as July 2021. Although initial exploitation capability existed earlier, the MOVEit campaign was executed in parallel with other major operations, including GoAnywhere MFT, reflecting a broader strategy of simultaneous mass exploitation across enterprise file transfer platforms.

---

### A. Initial Exploitation – CVE-2023-34362

CVE-2023-34362 is a SQL injection vulnerability affecting multiple versions of Progress MOVEit Transfer, including:

- 2021.0.6 (13.0.6) and earlier  
- 2021.1.4 (13.1.4)  
- 2022.0.4 (14.0.4)  
- 2022.1.5 (14.1.5)  
- 2023.0.1 (15.0.1)  

The vulnerability was publicly disclosed by Progress on May 31, 2023.

Exploitation of this flaw allows attackers to interact directly with backend database systems (MySQL, MS SQL Server, Azure SQL, etc.), enabling:

- Extraction of database schema information  
- Execution of malicious SQL queries  
- Modification, insertion, or deletion of database records  

This capability formed the primary entry point for the MOVEit Transfer compromise.

---

### B. Post-Exploitation Vulnerabilities – CVE-2023-35036 & CVE-2023-35708 Identified

Following initial exploitation, additional SQL injection vulnerabilities were identified in MOVEit Transfer:

- CVE-2023-35036  
- CVE-2023-35708  

These vulnerabilities allow unauthenticated attackers to directly access the MOVEit Transfer database via specially crafted HTTP requests targeting specific application endpoints.

Impact includes:

- Unauthorized database access  
- Data manipulation and extraction  
- Expansion of control over compromised environments  

These vulnerabilities further amplified the scale and efficiency of the mass data exfiltration campaign observed in 2023.

---

### C. Post-Exploitation Activity and Persistence Mechanism

Following successful exploitation, the threat actors established persistence within compromised MOVEit Transfer environments through deployment of a web shell. This allowed continued access while evading detection and supporting further malicious activity, including data collection and exfiltration.

In observed cases, the attack chain involved legitimate Windows processes such as `svchost.exe`, which initiated the IIS worker process `w3wp.exe`. This process was then used to generate multiple files within a newly created working directory in the system’s Temp directory. These files followed a pseudo-random naming pattern (eight-character identifiers), including payloads such as `human2.aspx`.

Further analysis of IIS logs indicated the use of:

- `moveitisapi.dll` – leveraged to execute SQL injection via crafted HTTP headers  
- `guestaccess.aspx` – used to establish sessions, extract CSRF tokens, and retrieve required parameters for further exploitation  

---

### D. Post-Exploitation Capabilities

Once initial access and persistence were established, attackers performed extensive database and system-level operations, including:

- Extraction of Microsoft Azure configuration data  
- Enumeration of SQL database contents  
- File creation, retrieval, and manipulation  
- Creation of unauthorized administrator accounts  
- Deletion of specific user accounts  

These actions demonstrate full application-level compromise with direct control over sensitive backend systems.

---

### E. Extortion Activity

Unlike previous TA505 ransomware campaigns, no ransomware payload was deployed in this operation. Instead, the focus remained on large-scale data theft and extortion.

Victims were subsequently contacted and instructed to pay ransom demands by June 14, 2023, under threat of public data exposure. This represents a shift toward pure data extortion rather than traditional encryption-based ransomware deployment.

