## first step to download it  ?
1. sudo apt update 
2. sudo apt install suricata -y
3. sudo suricata-update ( to update the database of rules)
4. sudo touch /var/lib/suricata/rules/local.rules
5. sudo suricata-update
6. sudo nano /etc/suricata/suricata.yaml (to edit the settings )
     * HOME_NET (Ching this to your ip)
     * search for cntrl +w  (rule-files) and add (- local.rules under suricata rules)
     * search for cntrl +w  (interface) and add yours
     * search for cntrl +w  (outpus(2)) and add ( types: ^alert under  types or filename)
     * 
     * sudo suricata -T -c /etc/suricata/suricata.yaml -v   ( for check the file of yaml )
     * ![](Attachments/Pasted%20image%2020260901034825.png)
     * sudo nano /var/lib/suricata/rules/local.rules ( to add rules for testing )
     * ![](Attachments/Pasted%20image%2020260901035614.png)\
     * └─$ sudo systemctl  status  suricata
       ![](Attachments/Pasted%20image%2020260901035956.png)
     * To monitor the appearance of notifications in real time>(sudo tail -f /var/log/suricata/fast.log)





___
___
___
 the second step set it with any one of the (SIEM) We will take the (Wazuh )
 1. sudo  nano / var/ossec/etc/ossec.conf/
 ```
 <!-- Suricata Log Collection -->
  <localfile>
    <log_format>json</log_format>
    <location>/var/log/suricata/eve.json</location>
  </localfile>
 ```
 2.  restart the wazuh agent 







___
___
___
## What is the difference between pfSense and Suricata?
1. pfSense Firewall asks: >> Is this connection allowed or blocked?
2. Meanwhile, Suricata asks: >> Does this communication seem like an attack or malicious activity?
		*Firewall sees rules and policies, while IDS/IPS sees the content and behavior of the attack*





ثم تأكد من تفعيل خيار التعطيل (**Disable**) لهذه الثلاثة: ?
1. ### 1. Hardware Checksum Offloading

### 2. Hardware TCP Segmentation Offloading (TSO)

### 3. Hardware Large Receive Offloading (LRO)
## لماذا؟

لأن هذه التقنيات تجعل **كرت الشبكة يعالج أو يغيّر بعض تفاصيل الـ Packets** لتسريع الأداء.

لكن Suricata يحتاج أن يرى الـ Packets بشكل صحيح لتحليلها:

System → Advanced → Networking




















___
___
# Suricata in Windows 
1. install the pacap 
2. C:\Program Files\Suricata    >> set the configration of suricata.yemel
![](Attachments/Pasted%20image%2020260913235847.png)
3.  search for (af-packet) and put the interface of internet
4. download the rules  of emarging
5. add rules to the files of rules 
6. in yemel search for (rule-file) add the name of the downloaded  rules file  
7. run in cmd as ADministrator and write the (cd  program files\suricata >>  "suricata -c suricata.yaml -i ethernet0")
8.   test the configration run the "suricata.exe -T -c suricata.yaml"




cd "C:\Program Files\Suricata"
.\suricata.exe -c suricata.yaml -k none --pcap  لتشغيلها في  ويندوز 1


cd "C:\Program Files\Suricata"
.\suricata.exe -c suricata.yaml -k none --pcap     لتشغيل السيروكاتا