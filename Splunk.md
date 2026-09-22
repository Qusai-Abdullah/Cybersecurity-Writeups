## what is the **Splunk** ?
is a leading data intelligence and Security Information and Event Management (**SIEM**) platform designed to collect, index, search, and analyze machine-generated data and logs in real-time. By utilizing its proprietary Search Processing Language (**SPL**), Splunk enables security analysts to correlate disparate events across the infrastructure, detect anomalies and cyber threats, visualize operational metrics through custom dashboards, and conduct in-depth digital forensics and incident investigation.




First thing is setup the splunk ?
![](Attachments/Pasted%20image%2020260907173052.png)

![](Attachments/Pasted%20image%2020260907174411.png)
## The step to set all setting and collection data  ?
1. setup the splunk to monitor the localhost
![](Attachments/Pasted%20image%2020260907174636.png)

2. 
![](Attachments/Pasted%20image%2020260907174734.png)
- **Upload (One-time ingestion):** Used to manually upload static, historical log files or structured data (e.g., `.csv`, `.log`, `.json`) directly from your machine for immediate, one-off analysis without continuous updates.
    
      
    
- **Monitor (Local continuous tracking):** Configures Splunk to listen to and continuously collect data in real time from the local machine it is installed on (e.g., local Windows Event Logs, specific local folders, local ports, or running scripts).
    
      
    
- **Forward (Remote agent collection):** Ingests live data sent from remote endpoints over the network using **Splunk Universal Forwarders** or **Heavy Forwarders** (e.g., remote domain controllers, endpoints, or network appliances streaming to port `9997`).
3. ![](Attachments/Pasted%20image%2020260907175600.png)
4. 
![](Attachments/Pasted%20image%2020260907180459.png)

> **Figure:** Configuring Windows Local Event Logs Ingestion in Splunk Enterprise.
> **Purpose:** To define and select critical Windows Event Log channels (specifically **Security**, **System**, and **Application**) for continuous real-time log ingestion and indexing directly on the host machine. The primary objective is to facilitate centralized threat monitoring, audit authentication events (e.g., Event IDs 4624/4625), track newly installed services, and establish visibility for subsequent forensic analysis and security correlation.


5. 
![](Attachments/Pasted%20image%2020260907193332.png)

6. ![](Attachments/Pasted%20image%2020260907193704.png)
THIS  is localhost  Above 
___
___
___

### How can I  collect the data from the Agent ?

1. select *Forwarding and receiving *  
![](Attachments/Pasted%20image%2020260907194955.png)

2. Receive data    +   add new ![](Attachments/Pasted%20image%2020260907195217.png)

3. The next step is to install the Universal Forwarder on the other device: <mark style="background: #FF5582A6;"><<<<</mark>
![](Attachments/Pasted%20image%2020260907202355.png)
4. 
![](Attachments/Pasted%20image%2020260907202607.png)
 

5. Open the command prompt (CMD) as administrator on this server, and navigate to the installation path:

```
splunk.exe add forward-server 192.168.10.128:9997
```

![](Attachments/Pasted%20image%2020260907203945.png)


C:\Program Files\SplunkUniversalForwarder\etc\system\local 
   Enter into *inputs.conf*

```
[WinEventLog://Security]
disabled = 0

[WinEventLog://System]
disabled = 0

[WinEventLog://Application]
disabled = 0       and save it
```   

![](Attachments/Pasted%20image%2020260907204756.png)
					 Than Restart (splunk.exe restart)
```
splunk.exe restart
```






6. ![](Attachments/Pasted%20image%2020260907194740.png) 

in the agent ?
C:\Program Files\SplunkUniversalForwarder\
cd "C:\Program Files\SplunkUniversalForwarder\bin"
splunk add forward-server 192.168.10.20:9997
splunk restart
splunk list forward-server

### الآن الخطوة التالية

نحن لم نرسل Logs بعد. الآن نحتاج أن نقول للـForwarder:

> اقرأ ملف Suricata `eve.json` وأرسله إلى Splunk.









# Splunk  in windows 
|الملف|السؤال الذي يجيب عليه|
|---|---|
|`inputs.conf`|**What should I collect?**|
|`outputs.conf`|**Where should I send it?**|



## إعداد Forwarder على Windows
1. C:\Program Files\SplunkUniversalForwarder\etc\system\local\

_طريقة بديلة عبر PowerShell / CMD كمسؤول:_

DOS

```
cd "C:\Program Files\Splunk\bin"
splunk status
```




splunk add forward-server 192.168.10.50:9997 لربط السبلانك في الفوروردر


splunk list forward-server لتاكيد من الاتصال 

سننشئ الملف:

```
C:\Program Files\SplunkUniversalForwarder\etc\system\local\inputs.conf
```

يمكنك إنشاء المجلد/الملف من CMD.

نفذ:

```
mkdir "C:\Program Files\SplunkUniversalForwarder\etc\system\local"
```

ثم:

```
notepad "C:\Program Files\SplunkUniversalForwarder\etc\system\local\inputs.conf"
```

ضع داخله:

```
[WinEventLog://Security]
disabled = 0
index = windows
sourcetype = WinEventLog:Security
renderXml = 1

[WinEventLog://System]
disabled = 0
index = windows
sourcetype = WinEventLog:System
renderXml = 1

[WinEventLog://Application]
disabled = 0
index = windows
sourcetype = WinEventLog:Application
renderXml = 1
```

ثم **Save**.


### 2. تأكد أن الإعداد تم قراءته

نفذ:

```
splunk cmd btool inputs list --debug | findstr /I "WinEventLog"
```

يجب أن يظهر لك:

```
WinEventLog://Security
WinEventLog://System
WinEventLog://Application
```