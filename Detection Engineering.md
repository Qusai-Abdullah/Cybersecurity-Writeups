#Detection_Engineering #TryHackMe #Blue_Team

## Core Concepts Learned

### 1. What is Detection Engineering?
* **Definition:** The continuous process of building and operating threat intelligence analytics to identify potentially malicious activity or misconfigurations within an environment.
* **Modern Approach ([[Detection as Code]] - DaC):** Treating detection logic as code by adopting software engineering principles, such as Version Control and CI/CD automation workflows.

---

### 2. Detection Types Matrix

| Perspective | Detection Type | Core Mechanism | Key Benefit | Key Challenge |
| :--- | :--- | :--- | :--- | :--- |
| **Environment-based** | **Configuration Detection** | Identifies misalignments in network, asset, or identity domains against a known baseline. | Easiest to maintain in static environments. | High false positives in dynamic, fast-changing environments. |
| | **Modelling** | Defines baseline operations and triggers alerts on any deviations. | Effectively identifies unknown adversary activities. | Provides no immediate threat context during investigations. |
| **Threat-based** | **Indicator Detection** | Relies on known Indicators of Compromise ([[IOCs]]) like malicious IPs, domains, or hashes. | Fastest type of detection to create and deploy. | Retroactive in nature; easily bypassed when the adversary changes tools. |
| | **Threat Behaviour Detection** | Focuses on tactics, techniques, and procedures (**TTPs**) aligned with frameworks like [[MITRE ATT&CK]]. | Highly scalable; withstands the adversary's rate of infrastructure change. | Requires massive amounts of log data to achieve full coverage. |

---

### 3. Benefits of Detection as Code (DaC)
* **Vendor-Agnostic Flexibility:** Leveraging universal formats like **[[Sigma]]** and **[[YARA]]** allows detections to be deployed across various SIEM, EDR, and XDR platforms.
* **Test-Driven Development:** Automated testing catches blind spots and filters out false positives early before deploying rules into production.
* **Code Reusability:** Simplifies the workflow by allowing engineers to repurpose established detection patterns for new threats rather than starting from scratch.
### 4 . Detection Gap Analysis
* **Definition:** The initial step to identify key areas where threat detection can be improved within an environment (also known as **Threat Modelling** in this context).
* **Approaches:**
    * **Reactive:** Analyzing recent internal incident reports and lessons learned to find missed detection areas.
    * **Proactive:** Mapping potential attacks and TTPs using [[MITRE ATT&CK]] and threat intelligence sources.

---

### 5. Datasource Identification & Baseline Creation
* **Datasource Identification:** Mapping out what logs are currently available versus what is missing to detect specific threat risks.
* **Security Baselines:** Defining what "normal behaviour" looks like across all organizational devices before writing detections. Divided into two categories:
    1. **High-Level Baselines:** Broad, OS-independent standards guided by organizational security policies.
    2. **Technical Baselines:** OS-specific configuration standards outlining hardening, network activities, IAM, and application policies.

---

### 6. Log Collection & Rule Writing
* **Log Collection:** Aggregating logs and metadata into a centralized system (SIEM) using network sensors and host tools like [[Sysmon]].
* **Rule Writing:** Creating logic to test for abnormal patterns against the logged events:
    * **Network Traffic:** Assessed via **[[Snort]]** rules.
    * **File Data:** Evaluated via **[[YARA]]** rules.
    * **Log Files:** Written using **[[Sigma]]** (a generic signature language).

---

### 7. Deployment, Automation & Tuning
* **Production & Maintenance:** Deploying tested rules into live environments and continuously modifying them to account for new attack patterns or infrastructure changes. It emphasizes viewing detection as an ongoing, iterative process.
