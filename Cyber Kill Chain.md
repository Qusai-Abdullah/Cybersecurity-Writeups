it is a military concept related to the structure of  an attack .  It consists of target identification

Thanks to Lockheed Martin, a global security and aerospace company, that established the Cyber Kill Chain® framework for the cybersecurity industry in 2011 based on the military concept. The framework defines the steps used by adversaries or malicious actors in cyberspace

<mark style="background: #FF5582A6;">### Why Is It Important to Understand How Cyber Kill Chain Works?</mark>
The Cyber Kill Chain will help you understand and protect against ransomware attacks, security breaches as well as Advanced Persistent Threats (APTs). You can use the Cyber Kill Chain to assess your network and system security by identifying missing security controls and closing certain security gaps based on your company's infrastructure.

By understanding the Kill Chain as a SOC Analyst, Security Researcher, Threat Hunter, or Incident Responder, you will be able to recognize the intrusion attempts and understand the intruder's goals and objectives. 
___
___
We will be exploring the following attack phases in this :
- Reconnaissance
- Weaponization
- Delivery
- Exploitation
- Installation
- Command & Control
- Actions on Objectives



#### Reconnaissance  
![](Attachments/Pasted%20image%2020260720222348.png)




___
___

### Weaponization
After a successful reconnaissance stage, "Megatron" would work on turning the raw information into actionable attack tools through crafting **malware** and **exploits** into a **payload**. Most attackers usually use automated tools to generate the malware or refer to the [DarkWeb(opens in new tab)](https://www.kaspersky.com/resource-center/threats/deep-web) to purchase the malware. More sophisticated actors or nation-sponsored APT (Advanced Persistent Threat Groups) would write their custom malware to make the malware sample unique and evade detection on the target.

![](Attachments/Pasted%20image%2020260722212417.png)

## let's define some key terminology.
**Malware** is a program or software that is designed to damage, disrupt, or gain unauthorized access to a computer.
**Exploits** are programs or code that take advantage of the vulnerability or flaw in the application or system.
**payload** is a malicious code that the attacker runs on the system.








___
___
### Delivery


![](Attachments/Pasted%20image%2020260722214246.png)
decides to choose the method for transmitting the payload or the malware onto the target environment

	there are many of options  to choose :
			Phishing email , USB drops
			Watering hole attacks : are targeted and designed to aim at a specific group of people by compromising the website they are usually visiting, redirecting them to a malicious website of the attacker's choice or creation.






___
___
### Exploitation
 is the moment the attacker's code executes on the target, taking advantage of a known vulnerability. In this phase, Megatron can opt to utilise a number of key techniques to gain access:

- Malicious macro execution: This may have been delivered through a phishing email, that would execute ransomware when the victim opens it.
- Zero-day exploits: These leverages on unknown and unpatched flaws in a system. These exploits leave no opportunity for detection at the beginning.
- Known CVEs: The attacker can choose to exploit unpatched public vulnerabilities found on the target environment.
After gaining access to the system, the malicious actor could exploit software, system, or server-based vulnerabilities to escalate the privileges or move laterally through the network. 


Signs of exploitation to look out for include:

- Unexpected process spawns.
- Registry changes or new services created.
- Suspicious command-line arguments found in system logs.

![](https://cdn-images.tryhackme.com/user-uploads/5c549500924ec576f953d9fc/room-content/df2135bd37c135a9c74cc83e43a1dc50.png)  
___
___
## Installation
![](Attachments/Pasted%20image%2020260722214442.png)
Once the attacker gets access to the system, he would want to reconnect back to the system if he loses the connection to it or if he got detected and got the initial access removed. Or if the system is later patched, they will no longer have access to it. That is when the attacker needs to install a **[persistent backdoor(opens in new tab)](https://www.offensive-security.com/metasploit-unleashed/persistent-backdoors/).** A persistent backdoor will let the attacker access the system he compromised in the past.


#### The persistence can be achieved through:
1. - Installing a **web shell** on the webserver. A web shell is a malicious script written in web development programming languages such as ASP, PHP, or JSP used by an attacker to maintain access to the compromised system. Because of the web shell simplicity and file formatting (.php, .asp, .aspx, .jsp, etc.) can be difficult to detect and might be classified as benign. You may check out this great article released by [Microsoft(opens in new tab)](https://www.microsoft.com/security/blog/2021/02/11/web-shell-attacks-continue-to-rise/) on various web shell attacks.
2.  Installing a backdoor on the victim's machine. For example, the attacker can use [Meterpreter(opens in new tab)](https://www.offensive-security.com/metasploit-unleashed/meterpreter-backdoor/) to install a backdoor on the victim's machine. Meterpreter is a Metasploit Framework payload that gives an interactive shell from which an attacker can interact with the victim's machine remotely and execute the malicious code.
3.  Creating or modifying Windows services. This technique is known as [T1543.003(opens in new tab)](https://attack.mitre.org/techniques/T1543/003/) on MITRE ATT&CK (MITRE ATT&CK® is a knowledge base of adversary tactics and techniques based on real-world scenarios). An attacker can create or modify the Windows services to execute the malicious scripts or payloads regularly as a part of the persistence. An attacker can use the tools like **ssc.exe** (sc.exe lets you Create, Start, Stop, Query, or Delete any Windows Service) and [Reg(opens in new tab)](https://attack.mitre.org/software/S0075/) to modify service configurations. The attacker can also **[masquerade(opens in new tab)](https://attack.mitre.org/techniques/T1036/)** the malicious payload by using a service name that is known to be related to the Operating System or legitimate software.
4. Adding the entry to the "run keys" for the malicious payload in the Registry or the Startup Folder. By doing that, the payload will execute each time the user logs in to the computer. According to MITRE ATT&CK, there is a startup folder location for individual user accounts and a system-wide startup folder that will be checked no matter what user account logs in.

>[!note  the link  is : so important link ]
[https://attack.mitre.org/techniques/T1547/001/ ]


>[!note  You can read more about the Registry Run Keys / Startup Folder persistence on one of the]
>[MITRE ATT&CK techniques(opens in new tab)](https://attack.mitre.org/techniques/T1547/001/).



![](Attachments/Pasted%20image%2020260722235804.png)

___
___
### Command & Control ?
After getting persistence and executing the malware on the victim's machine, Megatron opens up the C2 (Command and Control) channel through the malware to remotely control and manipulate the victim. This term is also known as **C&C or C2 Beaconing** as a type of malicious communication between a C&C server and malware on the infected host.

![](Attachments/Pasted%20image%2020260723000712.png)

The Compromised endpoint would communicate with a external server set up by an attacker to establish a command & control channel. After establishing the connection, the attacker has full control of the victim's machine.

### The most common C2 channels used by adversaries include:

- HTTP on port 80 and HTTPS on port 443, where this type of beaconing blends the malicious traffic with the legitimate traffic and can help the attacker evade firewalls.
    
- DNS (Domain Name Server), where the infected machine makes constant DNS requests to the DNS server that belongs to an attacker, this type of C2 communication is also known as DNS Tunneling


  What is the C2 communication where the victim makes regular DNS requests to a DNS server and domain which belong to an attacker. ???? 
   DNS Tunneling
___ 
___
### Actions & Objectives  (Exfiltration)?
After going through six phases of the attack, Megatron can finally achieve his goals, which means taking action on the original objectives. With hands-on keyboard access, the attacker can achieve the following: 

- Collect the credentials from users.
- Perform privilege escalation (gaining elevated access like domain administrator access from a workstation by exploiting the misconfiguration).
- Internal reconnaissance (for example, an attacker gets to interact with internal software to find its vulnerabilities).
- Lateral movement through the company's environment.
- Collect and exfiltrate sensitive data.
- Deleting the backups and shadow copies. Shadow Copy is a Microsoft technology that can create backup copies, snapshots of computer files, or volumes. 
- Overwrite or corrupt data.



![](Attachments/Pasted%20image%2020260723002556.png)




___
____
# Unified kill Chain 


### what is the Threat modelling ?
The UKC states that there are 18 phases to an attack: Everything from reconnaissance to data exfiltration and understanding an attacker's motive.

![](Attachments/Pasted%20image%2020260727020248.png)

1. **Reconnaissance ([MITRE Tactic TA0043](https://attack.mitre.org/tactics/TA0043/)**
This phase of the UKC describes techniques that an adversary employs to gather information relating to their target.

2. **Weaponization ([MITRE Tactic TA0001(opens in new tab)](https://attack.mitre.org/tactics/TA0001/))**
    This phase of the UKC describes the adversary setting up the necessary infrastructure to perform the attack.
3. **Social Engineering ([MITRE Tactic TA0001(opens in new tab)](https://attack.mitre.org/tactics/TA0001/))**
 This phase of the UKC describes techniques that an adversary can employ to manipulate employees to perform actions that will aid in the adversaries attac



























4. In what year was the Unified Kill Chain framework released?
2017

2. What is the name of the attack phase where an attacker employs techniques to evade detection? 
defense Evasion 

3. What is the name of the attack phase where an attacker employs techniques to remove data from a network?
 Exfiltration








