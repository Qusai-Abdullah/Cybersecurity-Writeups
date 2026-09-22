We will learn the following things 
- What is Wazuh and why is it a powerful unified security solution
- Where Wazuh is used and how to navigate it
- Learning about Wazuh rules and security alerts
- Digesting logs to view events on Linux and Windows
- How you can extend Wazuh using plugins and its API

default password of wazuh server is 
username = wazuh-user
password= wazuh

What does Wazuh mean ?
 it started as an EDR-focused tool, Wazuh has grown into a unified security platform that combines endpoint detection and response, event management, vulnerability assessment, and cloud security monitoring under one roof 
 Founded in 2015, [Wazuh(opens in new tab)](https://wazuh.com/) is used across organisations of all sizes - from small businesses to large enterprises and government institutions. Wazuh operates on a manager and agent model.




#### simple idea about wazuh ?
, there is one Wazuh server (**manager**) that stores and processes the data, and many hosts (**agents**) that send data to the manager. Let's look at this model in the diagram below:

![](Attachments/Pasted%20image%2020260729235937.png)
## what does Agent mean ?
Devices that record the events and processes of a system are called agents.
. Agents monitor the processes and events that take place on the device, such as authentication and user management. Agents will offload these logs to a designated collector 


# Wazuh’s Vulnerability Assessment modul ?
 is a powerful tool that can be used to periodically scan an agent's operating system for installed applications and their version numbers.

Wazuh is capable of auditing and monitoring an agent's configuration whilst proactively recording event logs. When the Wazuh agent is installed, an audit is performed where a metric is given using multiple frameworks and legislations such as NIST, MITRE and GDPR


![](Attachments/Pasted%20image%2020260730004249.png)



### Collecting Windows Logs with Wazuh ?

All sorts of actions and events are captured and recorded on a Windows operating system. This includes authentication attempts, networking connections, files that were accessed, and the behaviours of applications and services. This information is stored in the Windows event log using a tool called Sysmon.

#### ## We can use the Wazuh agent to aggregate these events recorded by _Sysmon_ for processing to the wazuh manage

 Now, we will need to configure both the Wazuh agent and the Sysmon application.  Sysmon uses rules that are made in XML formatting to be triggered. For example, in the XML snippet below, we are telling Sysmon to monitor for the event of the powershell.exe process starting.


![](Attachments/Pasted%20image%2020260730010913.png)




to lets sysmon working with  windows and  Wazuh we need to do some steps?
* execute the Sysmon application and provide the aforementioned configuration file like so 
* The command to Run its with its rules in file xml 
```
``` Sysmon64.exe -accepteula -i detect_powershell.xml ```
```
* if you have the Sysmon without the file configuration you should use this command 
* ```
  Sysmon64.exe -c sysmonconfig.xml
  
  
  
  it will show >> Loading configuration file with schema version 4.90
Configuration file validated.
Configuration updated.

  ```
* We can verify that Sysmon has accepted our configuration file by navigating to the Event Viewer and searching for the “**Sysmon**” module like so:
![](Attachments/Pasted%20image%2020260730011826.png)





![](Attachments/Pasted%20image%2020260730012224.png)



 1. Before preparation in my windows 
 

![](Attachments/Pasted%20image%2020260730015916.png)

2. after preparation in my windows 
![](Attachments/Pasted%20image%2020260730020826.png)


<mark style="background: #FF5582A6;">To stop the Sysmon ?</mark>
```
sc stop Sysmon64
``` 
___
___
And this is the place from which Wazuh or Splunk or any SIEM reads if you set up log collection.
Event Viewer
    └── Applications and Services Logs
          └── Microsoft
                └── Windows
                      └── Sysmon
                            └── Operational

___
___
<mark style="background: #FF5582A6;">How can you install The Agent from Wazuh to window ?</mark>
1.  ![](Attachments/Pasted%20image%2020260730025917.png)
2. ![](Attachments/Pasted%20image%2020260730032147.png)
<mark style="background: #FF5582A6;">3. To  ensure of service is running ?</mark>
	```
	   Get-Service wazuhsv
	   ss -tulpn | grep 1515   في السرفر حق الوازو
	   
	```
	

How  can you make sysmon with Agent ?
1. Open the PowerShell as administrator 
2. open the Notepad by
	notepad "C:\Program Files (x86)\ossec-agent\ossec.conf"
3. Scroll down and look for the log reading section localfile
4. Add the following code as a new section inside the settings file :
```<!-- Sysmon Events Collection -->
  <local file>
    <location>Microsoft-Windows-Sysmon/Operational</location>
    <log_format>eventchannel</log_format>
  </localfile>
 
5. save the file 
6. restart the Wazuh by : NET STOP Wazuh ; NET START Wazuh

```

![](Attachments/Pasted%20image%2020260730044640.png)




___
___

### Collecting Linux Logs with Wazuh

Capturing logs from a Linux agent is a simple process similar to capturing events from a Windows agent. We will be using Wazuh’s log collector service to create an entry on the agent to instruct what logs should be sent to the Wazuh management server.
Wazuh comes with many rules that enable Wazuh to analyze log files and can be found in `/var/ossec/ruleset/rules`. Some common applications include:
		        - Docker
				- FTP
				- WordPress
				- SQL Server
				- MongoDB
				- Firewall
				- And many, many more (approximately 900)



#### This ruleset can analyze apache2 logs for warnings and error messages like so: We will need to insert this into the Wazuh’s agent that is sending logs to the Wazuh management servers configuration file located in `/var/ossec/etc/ossec.conf`:

```<!-- Sysmon Events Collection -->
 <!-- Apache2 Log Analysis --> <localfile> <location>/var/log/example.log</location> <log_format>syslog</log_format> </localfile>

```

## What is the full file path to the rules located on a Wazuh management server?
/var/ossec/ruleset/rules




### What does **`auditd`** mean ?
The auditd tool (Linux Audit Daemon) is a built-in service in the Linux operating system that works as a sensor monitoring everything happening inside the system at the kernel level, such as:

- Modifying sensitive files.
- Running commands and programs.
- Changing user permissions or login attempts.

 1. First, we will need to install the `auditd` package and an `auditd` plugin?
```
sudo apt-get install auditd audispd-plugins
`sudo systemctl enable auditd.service` & `sudo systemctl start auditd.service`
```

2. we will be telling `auditd` to monitor for any commands executed as root.
3. `Auditd` rules are located in the following directory: `/etc/audit/rules.d/audit.rules`

```
1.sudo nano /etc/audit/rules.d/audit.rules
and appending 
2. `-a exit,always -F arch=64 -F euid=0 -S execve -k audit-wazuh-c`
```

![](Attachments/Pasted%20image%2020260731002158.png)

3. configure the Wazuh agent to detect this new log file that is generated by `auditd`
```
1- sudo nano /var/ossec/etc/ossec.conf
2- put your rules in the file .conf 
this is >>

<localfile> <location>/var/log/audit/audit.log</location> <log_format>audit</log_format> </localfile> >> "this line for Determining the format and method of analyzing records"

```


![](Attachments/Pasted%20image%2020260731012124.png)

```
systemctl restart wazuh-agent  >> this command to fix configuration of service

```

















What is the full path & filename for where the aforementioned application stores rules?
```
etc/audit/rules.d/audit.rules
```
















### Wazuh API











