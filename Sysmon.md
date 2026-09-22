








Sysmon64.exe -accepteula -i  >>     -i for Install   
 ![](Attachments/Pasted%20image%2020260907135636.png)




2. ![](Attachments/Pasted%20image%2020260907140109.png)



3. ![](Attachments/Pasted%20image%2020260907140326.png)



<localfile>
    <location>Microsoft-Windows-Sysmon/Operational</location>
    <log_format>eventchannel</log_format>
</localfile>   


[WinEventLog://Microsoft-Windows-Sysmon/Operational]
disabled = 0
renderXml = 1
index = sysmon
sourcetype = XmlWinEventLog:Microsoft-Windows-Sysmon/Operational 



& "C:\Program Files\Splunk\bin\splunk.exe" restart

___
___
## ZEEK


/usr/local/bin/zeekctl status   ..>> for  ensure  the zeek

sockstat -46L | grep 9991 >> لمعرفه من يستخدم هذا  البورت 

![](Attachments/Pasted%20image%2020260907152721.png)

![](Attachments/Pasted%20image%2020260907152834.png)


Zeek يحاول معرفة نوع الخدمة من **سلوك البروتوكول نفسه**، وليس فقط من رقم المنفذ.