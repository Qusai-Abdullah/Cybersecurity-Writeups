- **Concept:** A conceptual framework used in Cyber Defense and Threat Intelligence to measure how difficult it is for an attacker to change their Indicators of Compromise (IoCs) when defenders detect and block them.
    
- **Core Goal:** To shift a defender's focus from tracking easy-to-change indicators (like Hashes and IPs) to detecting attacker behaviors and methodologies (**TTPs**), which inflicts the maximum amount of "pain" on the adversary.



<mark style="background: #FF5582A6;">Are you ready to explore what hides inside the Pyramid of Pain?</mark> 
## Hash Values (Trivial) 
1. the hash value is a numeric value of a fixed length that uniquely identifies data. A hash value is the result of a hashing algorithm.
	 Tpye of Hashes 
	* **MD5 (Message Digest, defined by [RFC 1321(opens in new tab)](https://www.ietf.org/rfc/rfc1321.txt)****)** - was designed by Ron Rivest in 1992 and is a widely used cryptographic hash function with a 128-bit hash value. MD5 hashes are **NOT** considered **cryptographically secure**
	* SHA-1 (Secure Hash Algorithm 1, defined by [RFC 3174(opens in new tab)](https://tools.ietf.org/html/rfc3174)- was invented by United States National Security Agency in 1995. When data is fed to SHA-1 Hashing Algorithm, SHA-1 takes an input and produces a 160-bit hash value string as a 40 digit hexadecimal number. [NIST deprecated the use of SHA-1 in 2011(opens in new tab)](https://csrc.nist.gov/news/2017/research-results-on-sha-1-collisions) and banned its use for digital signatures at the end of 2013 based on it being susceptible to brute-force attacks. Instead, NIST recommends migrating from SHA-1 to stronger hash algorithms in the SHA-2 and SHA-3
	* - **The SHA-2 (Secure Hash Algorithm 2)** - SHA-2 Hashing Algorithm was designed by The National Institute of Standards and Technology (NIST) and the National Security Agency (NSA) in 2001 to replace SHA-1. SHA-2 has many variants, and arguably the most common is SHA-256. The SHA-256 algorithm returns a hash value of 256-bits as a 64 digit hexadecimal number.

>[! A hash is not considered to be cryptographically secure if two files have the same hash value or digest. ] 


GOOT TOOLS OR Functions useful for all above ?
* GET-FileHahe 
* [metadefender.com](https://metadefender.com/)
* https://www.virustotal.com/
---

### Ip Address (Easy)
An IP address is used to identify any device connected to a network. These devices range from desktops, to servers and even CCTV cameras! We rely on IP addresses to send and receive the information over the network. But we are not going to get into the structure and functionality of the IP address. As a part of the Pyramid of Pain, we’ll evaluate how IP addresses are used as an indicator.

One of the ways an adversary can make it challenging to successfully carry out IP blocking is by using  *<mark style="background: #D2B3FFA6;">*Fast Flux.**</mark>

## What is the  Fast Flux?
 is a DNS technique used by botnets to hide phishing, web proxying, malware delivery, and malware communication activities behind compromised hosts acting as proxies. The purpose of using the Fast Flux network is to make the communication between malware and its command and control server (C&C) challenging to be discovered by security professionals.
___
### Domain Names (Simple)





what is the Punycode ?
Punycode attack used by the attackers to redirect users to a malicious domain that seems legitimate at first glance.


### what is preview ?
هي عملية عرض معلومات أو محتوى مسبقًا قبل فتحه أو الوصول إليه، وذلك لمساعدة المستخدم على التحقق مما سيحدث. باستخدام perview قبل  اسم  الموقع مثال :
https://preview.tinyurl.com/bw7t8p4u
او اضافه + نهاية الرابط 

- يحول أسماء النطاقات التي تحتوي على أحرف Unicode إلى صيغة ASCII تبدأ غالباً بـ **`xn--`**، وقد يستغلها المهاجمون في هجمات **Homograph** لإنشاء مواقع تبدو مطابقة للمواقع الأصلية.
- يمكن اكتشاف النطاقات المشبوهة عبر **Proxy Logs** و **Web Server Logs**.
- يستخدم المهاجمون خدمات **اختصار الروابط** مثل **bit.ly** لإخفاء الوجهة الحقيقية للرابط.


## مثال 2

```
tryhackme.evilcorp.com
```

يتكون من

```
tryhackme = Subdomain

evilcorp = Domain

com = Top Level Domain
```

إذن

```
Subdomain.Domain.TLD
```





### Host Artifacts (Annoying) ?
this level, the attacker will feel a little more annoyed and frustrated if you can detect the attack
Host artifacts are the traces or observables that attackers leave on the system
* such as registry values, suspicious process execution, attack patterns or IOCs (Indicators of Compromise), files dropped by malicious applications, or anything exclusive to the current threat.
* **Suspicious process execution from Word:**
 ![](Attachments/Pasted%20image%2020260717033509.png)
* **Suspicious events followed by opening a malicious application:**
![](Attachments/Pasted%20image%2020260717033630.png)


### Network Artifacts (Annoying) ?
Network Artifacts also belong to the yellow zone in the Pyramid of Pain. This means if you can detect and respond to the threat, the attacker would need more time to go back and change his tactics or modify the tools, which gives you more time to respond and detect the upcoming threats or remediate the existing ones.

A network artifact can be a user-agent string, C2 information, or URI patterns followed by the HTTP POST requests.An attacker might use a User-Agent string that hasn’t been observed in your environment before or seems out of the ordinary.

Network artifacts can be detected in PCAPs (file that contains the network packet dumps) by using a tool such as Wireshark or TShark, or exploring IDS (Intrusion Detection System) alerts from a tool such as [Snort(opens in new tab)](https://www.snort.org/).
![](Attachments/Pasted%20image%2020260717041041.png)
 
 
## Tools (Challenging)

At the **Tools** level of the Pyramid of Pain, defenders focus on detecting the actual tools used by attackers rather than simple indicators like IP addresses or domains. These tools include malware, backdoors, malicious documents (Maldocs), payloads, DLLs, EXE files, and password crackers.

Detecting an attacker’s tools is highly effective because replacing or rewriting them requires significant time, effort, and resources. As a result, attackers may need to develop new malware or switch to entirely different toolsets.

### Detection Methods
- **Antivirus Signatures:** Detect known malware based on predefined signatures.
- **YARA Rules:** Identify malware by matching unique strings, patterns, or file characteristics.
- **Detection Rules:** SIEM rules (e.g., Splunk, Sigma, Sentinel) used to detect malicious tools and behaviors.
- **Malware Repositories:** Platforms such as **MalwareBazaar** and **MalShare** provide malware samples, threat intelligence, and YARA rules for analysis.
- **SOC Prime:** A marketplace where security researchers share detection rules for malware and exploited CVEs. https://tdm.socprime.com/signup
- ![](Attachments/Pasted%20image%2020260720015044.png)

### Fuzzy Hashing
Unlike traditional hashes (MD5, SHA1, SHA256), which change completely after even a single-byte modification, **Fuzzy Hashing** measures the similarity between files.

It is commonly used to identify modified versions of malware that share the same code base. One of the most widely used fuzzy hashing algorithms is **SSDeep**, which compares files and returns a similarity percentage.

**Alternative name:** Context Triggered Piecewise Hashing (CTPH)

### Key Takeaways
- Detecting attacker tools significantly increases the attacker's operational cost.
- YARA is one of the most powerful techniques for malware detection and threat hunting.
- Fuzzy Hashing helps identify malware variants even when their cryptographic hashes differ.
- Combining signatures, YARA rules, behavioral detection, and threat intelligence provides stronger protection against attacker tools.


<mark style="background: #FF5582A6;">## How to Prevent Pass-the-Hash Attacks  ?</mark>
For a PtH attack to succeed, the perpetrator must first gain local administrative access on a computer to lift the hash. Once the attacker has a foothold, they can move laterally with relative ease, lifting more credentials and causing [privilege escalation](https://www.beyondtrust.com/blog/entry/privilege-escalation-attack-defense-explained) along the way.

Implementing the following security best practices will help eliminate, or at least minimize, the impact of a PtH attack:

- [Least Privilege Security Model](https://www.beyondtrust.com/blog/entry/what-is-least-privilege): Limits the scope and mitigates the impact of a PtH attack by reducing an attacker's ability to escalate privileged access and permissions. Removing unnecessary admin rights goes a long way in reducing the threat surface for PtH and many other types of attacks. 
    
- [Password Management Solutions](https://www.beyondtrust.com/password-management): Rotating passwords frequently (and/or after a known credential compromise) can condense the window of time during which a stolen hash remains valid. By automating password rotation to occur after each privileged session, you can completely thwart PtH attacks and other exploits that rely on password reuse. The use of [one-time-passwords (OTPs)](https://www.beyondtrust.com/blog/entry/one-time-password-otp-solutions-for-privileged-access) can also mitigate PtH threats, as an OTP may only be valid for a single login session.
    
- [Separation of Privileges](https://www.beyondtrust.com/resources/glossary/separation-of-privilege): Separating different types of privileged and non-privileged accounts can reduce the scope of usage for administrator accounts. It reduces the risks of compromise and opportunities for lateral movement.
-

___
___
## TTPs (Tough)

The **Tactics, Techniques, and Procedures (TTPs)** layer is the highest level of the Pyramid of Pain because it focuses on the attacker's behavior rather than easily changeable indicators such as IP addresses, domains, or file hashes.

TTPs describe the complete attack lifecycle and are documented in the **MITRE ATT&CK Framework**.

### Components
- **Tactics:** The attacker's objective (e.g., Initial Access, Persistence, Exfiltration).
- **Techniques:** The methods used to achieve that objective (e.g., Pass-the-Hash, PowerShell, Credential Dumping).
- **Procedures:** The specific implementation, tools, or commands used by the attacker.

### Why TTPs Matter
Detecting attacker behavior forces adversaries to redesign their attack methodology instead of simply changing malware, domains, or infrastructure. This significantly increases the attacker's cost and effort.

### Detection Methods
- Behavioral Analytics
- Windows Event Log Monitoring
- SIEM Detection Rules (Splunk, Sentinel, Elastic)
- MITRE ATT&CK Mapping
- Threat Hunting
- EDR/XDR Telemetry

### Example
A **Pass-the-Hash** attack can be detected by monitoring Windows authentication events, NTLM logins, privilege escalation, and lateral movement activities. Detecting this behavior early allows defenders to isolate compromised hosts before attackers move further within the network.

### Key Takeaways
- TTP detection focuses on attacker behavior rather than indicators.
- MITRE ATT&CK is the primary framework for mapping and understanding TTPs.
- Behavioral detection is more resilient than signature-based detection.
- Detecting TTPs greatly increases the attacker's operational cost and often forces them to abandon the attack.





![](Attachments/Pasted%20image%2020260720023004.png)




