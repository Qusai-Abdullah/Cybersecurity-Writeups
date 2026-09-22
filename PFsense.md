

What is the PFSense ?
An open-source firewall and router platform used to secure and manage networks.

![](Attachments/Pasted%20image%2020260810023334.png)


You need to give the firewall two interfaces: an internal network interface and an external network interface. 
WAN =192.168.8.10  gateway =192.168.8.1 
LAN =192.168.10.1  with no gateway    this is for connect and manager the firewall from web>>
this is all configuration i had made 

![](Attachments/Pasted%20image%2020260810023828.png)


The most important step is 
## 1. Install Important pfSense Packages

The following packages are useful for improving firewall security, web filtering, and network monitoring.

### 1.1 Squid

**Squid** is a web proxy and caching server that can be used to control and monitor HTTP/HTTPS web traffic.

**Main benefits:**

- Acts as a proxy between clients and the Internet.
- Provides web traffic control.
- Can be used for caching frequently accessed content.
- Helps administrators monitor and control web access.

---

### 1.2 SquidGuard

**SquidGuard** is a URL filtering tool that works with Squid to control which websites users can access.

**Main benefits:**

- Blocks unwanted or inappropriate websites.
- Allows URL/domain-based filtering.
- Can create access-control policies for different users or networks.
- Can help enforce an organization's web browsing policy.

> **Note:** SquidGuard depends on Squid and is mainly useful when you specifically need URL-based web filtering.

---

### 1.3 Suricata ⭐

**Suricata** is a high-performance **Network IDS/IPS (Intrusion Detection and Prevention System)**.

**Main benefits:**

- Detects suspicious and malicious network traffic.
- Uses rules/signatures to identify attacks.
- Can operate as **IDS** to detect and alert.
- Can operate as **IPS** to detect and block traffic.
- Provides detailed network security logs.
- Can be integrated with security monitoring platforms such as **Wazuh** and **Splunk**.

---

### 1.4 pfBlockerNG-devel ⭐

**pfBlockerNG** provides **IP and DNS-based filtering** and can use threat-intelligence feeds to block known malicious IP addresses and domains.

**Main benefits:**

- Blocks malicious IP addresses.
- Blocks malicious or unwanted domains.
- Can use external threat-intelligence feeds.
- Helps reduce exposure to known malicious infrastructure.
- Can provide DNS-based filtering.
![467](Attachments/Pasted%20image%2020260810031842.png)

1![447](Attachments/Pasted%20image%2020260810024923.png)  
2
![456](Attachments/Pasted%20image%2020260810025041.png)
3 its starts with download 
![458](Attachments/Pasted%20image%2020260810025201.png)
4 ![450](Attachments/Pasted%20image%2020260810030247.png)
***its success***

___
___

From here all Downloaded Package 
![](Attachments/Pasted%20image%2020260810024529.png)
to ensure all of that downloaded loke at **Services** + look to the list as below !!
![](Attachments/Pasted%20image%2020260810030059.png)



___
___
 ##What Does the **Blocklist / Allow list**. / **IOC List** mean  or The difference between the them? 
 1.  <mark style="background: #FF5582A6;">Blocklist</mark> >> > A list of IP addresses, domains, or other entities that are explicitly blocked.
 2. <mark style="background: #FF5582A6;">Allowlist</mark> >> >  A list of trusted IP addresses, domains, or devices that are explicitly allowed.
 3. *<mark style="background: #FF5582A6;">*IOC List   </mark>  >> > A list of Indicators of Compromise (IOCs) associated with malicious or suspicious activity.
 
**In short** 
Allowlist → What do I allow? ✅
Blocklist → What do I block? 🚫
IOC List → What is associated with a threat or breach?



1. <mark style="background: #FF5582A6;">ShallaList</mark> >> > > ShallaList is a categorized URL and domain blacklist used for web content filtering. 
##### What are its benefits ?
It contains categories such as:
Adult → Adult Content
Gambling → Gambling
Malware → Malware
Phishing → Phishing
Social Networks → Social Networks
Games → Games
> [!NOTE]  
> **Note:** Shallalist has become outdated and has largely been replaced by **HaGeZi**.



pkg-static update -f
pkg-static upgrade -f
pkg-static install pfSense-pkg-squid





___
___
___
pfSense
qusai123456789@
pfSense_OU 





لاضافه المستخدم او عمل اتصال بين ال AD   with pfSense 

1. system >user manager > authentication servers >  add >






____
___
___


سبب انقطاع الويب الخاص بالكونسول لل pfsense i هو ال جيت واي الخاص بالويندوز نفسه الكلاينت   نخليه على نفس ال lan for pfsense 



سبب عدم قبل اي اسم مستخدم في الويندوز  WINDOWS1  ولا حتى ال  (administrator  الخاص بال AD)   , ولا حتى قبل اي مستخدم يسجل عبر  الويندوز حتى لو هو مسجل عبر ال  ال AD ???


هو انه موجه عبر ال DNS  الى مكان غير  مكان ال Active directory DNS  



تاسبب الرئيسي لعدم قدرة الOpenvpn الاتصال  وضهور الخطوط الحمراء وهو انه  ال WLN  حقها الايبي مختلف في ال pfsense    


username = .\Lab1
password =123

___
___
___




مستخدم في المنضمه الخاصه بال pfsense   
pp
qusai12345678

qusai20 
mohammed123456789@




هنا ساره 
![](Attachments/Pasted%20image%2020260831023719.png)


___
___

sAMAccountName 
هذا مهم جدًا للمستخدمين.

```
sAMAccountName
```

يعني أن pfSense عندما يستقبل:

```
Username: ahmed
```

سيبحث في AD عن:

```
sAMAccountName=ahmed
```



___
___
# openVPN ?






بناءً على الصورة، الفرق بين خيارات المصادقة هو:

- **Local User Access**: يتم تخزين المستخدمين وكلمات المرور محلياً على جهاز الخادم نفسه.
- **LDAP**: يتم المصادقة عبر خادم LDAP خارجي (مثل Active Directory).
- **RADIUS**: يتم المصادقة عبر خادم RADIUS خارجي (غالباً لشبكات المؤسسات أو مزودي الخدمة).

**الخلاصة**: "Local" يعتمد على الخادم نفسه، بينما LDAP و RADIUS يعتمدان على خوادم خارجية لإدارة المستخدمين.