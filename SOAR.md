
SOAR(Security Orchestration , Automation ,and Response)
To defend against attacks, a SOC team relies on various security solutions, such as SIEM, EDR, firewalls, and threat intelligence platforms. They also communicate with IT and management teams as part of their processes. However, as threats grow more complex and advanced, SOC teams face challenges like alert fatigue, manual processes, too many disconnected tools, and difficulties in communication across teams.

## Learning Objectives

- Understand the traditional SOC and its challenges
- Explore how SOAR overcomes these challenges
- Learn SOAR Playbooks
- Practically walk through a threat intelligence workflow

## How Traditional SOCs Work ?
Before we dive into learning the SOAR tool, let's take a look at how traditional Security Operations Centers (SOC) work and the challenges they face.

## Challenges Faced by SOCs ?
1. Alert Fatigue >>
2. Too many Disconnected Tools
3. Talent Shortage
4. Manual processes


we will learn about a tool that can overcome these challenges for a SOC team. This tool is called Security Orchestration, Automation, and Response (SOAR).
 Let's discuss what this tool is and how it overcomes these challenges. 
 
<mark style="background: #FF5582A6;">### What is SOAR ?</mark>
is a tool unifies all security tools used in a (SOC)  With SOAR ..
SOC analysts do not need to switch between (SIEM , EDR , Firewall) and other security tools for their investigations. >> They can operate all these tools within a single SOAR interface.

<mark style="background: #FF5582A6;">  The core strength  of a SOAR Tool comes from following three  main capabilities ?</mark>
#### 1. Orchestration 
* .a SOC analyst has to switch between multiple security tools for the analysis. For example, during a VPN brute force, the analyst typically switches between the following tools:

* . **SIEM** to check if the user usually uses the subject IP for logging
*  **Threat Intelligence (TI) platforms** to verify the IP's reputation
*  **IAM tool** to disable the user if there was any successful attempt
*  **Ticketing system** to open and track the incident 

*This manual switching between different tools slows down the process*. Orchestration <mark style="background: #FFF3A3A6;">solves</mark> this problem by coordinating all these tools together inside the SOAR. It connects different tools from various vendors within the unified SOAR interface. It defines workflows for investigating various types of alerts, known as **Playbooks**. These <mark style="background: #FF5582A6;">playbooks</mark> are predefined steps that tell the SOAR how to investigate an alert.
 >[!Example] 🧪
 the VPN brute force alert we discussed above would have the following playbook: >>

```
1. Received alert from SIEM
2. Query SIEM to check if the User normally uses the IP
3. Check TI platforms for the IP's reputation 
4. Query SIEM for any successful logins 
5. Escalate to containment actions
   
   
	The above actions are predefined in a playbook for a specific alert.
```

## 2. Automation ?
The art of coordinating with multiple tools through predefined actions (Playbooks), which we studied in Orchestration, can be automated. Automation means no more manual clicks needed from SOC analysts. SOAR will itself follow the playbooks.

>[!Example] 🧪 
>  Let's resume the playbook for VPN brute force alert combined with the Automation.


1. SOAR receives the alert from SIEM
2. It automatically queries the SIEM for the user's historical logins
3. It automatically verifies the IP's reputation through TI platforms
4. If the IP is malicious, it automatically disables the user from the IAM
5. Lastly, it automatically opens a ticket in the ticketing system with all the details to initiate an investigation

This saves a tremendous amount of time for SOC analysts. They can handle hundreds of alerts without burning out.

## 3. Response ?
SOAR gives the ability to take actions using different tools from one unified interface. It also automates the response, as we saw earlier while looking at its Automation capability. For example, SOAR can follow the playbook of VPN Brute force and block the IP on the firewall, disable the user in the IAM, and open a ticket with all the details.


The Orchestration, Automation, and Response capabilities of SOAR solve the major challenges a SOC team faces. With SOAR, there is no more alert fatigue, most of the processes are automated, and all the different tools are connected for coordination.

![](Attachments/Pasted%20image%2020260713162850.png)


<mark style="background: #FF5582A6;">## Do We Still Need SOC Analysts?</mark>

While a SOAR tool can automate the majority of repetitive tasks, it does not replace SOC analysts. Complex investigations still require an SOC analyst. SOAR cannot give a judgment call at some critical points, but an analyst can. A SOC analyst understands the threats in the broader business context. The playbooks for different types of alerts are also made by the SOC analysts. So, the answer to this question is that the SOAR would ease the burden of SOC by automating repetitive tasks and organizing everything in a simplified structure, but we still need SOC analysts.




# SOAR Playbooks

## What is a SOAR Playbook?

A SOAR Playbook is a predefined workflow that defines the actions a SOAR platform should take when a specific security alert occurs. It automates repetitive SOC tasks and guides analysts through the investigation and response process.

---

## Phishing Playbook

Phishing attacks are one of the most common attack vectors. Investigating phishing emails manually requires time to analyze URLs, attachments, and verify threats using Threat Intelligence platforms.

A Phishing Playbook automates this process:

- Receive a suspicious email alert.
    
- Create an incident ticket.
    
- Check if the email contains URLs or attachments.
    
- Analyze URLs using Threat Intelligence.
    
- Analyze attachments using malware analysis tools.
    
- If malicious, perform remediation actions:
    
    - Block malicious URLs.
        
    - Remove phishing emails.
        
    - Notify affected users.
        

---

## CVE Patching Playbook

A CVE (Common Vulnerabilities and Exposures) is a publicly disclosed vulnerability assigned a unique identifier.

CVE Patching Playbooks help automate vulnerability management:

- Receive information about a new CVE.
    
- Analyze vulnerability details and severity.
    
- Check whether affected systems exist in the environment.
    
- Create a patching ticket.
    
- Test the patch.
    
- Deploy the patch to production after approval.
    

---

## Role of SOC Analysts

Although SOAR automates many repetitive tasks, SOC analysts are still required for important decisions, such as:

- Reviewing investigation results.
    
- Approving critical actions.
    
- Validating remediation steps.
    

SOAR improves SOC efficiency by reducing manual work, speeding up response time, and providing consistent incident handling procedures.
