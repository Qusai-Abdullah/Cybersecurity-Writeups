> **SNORT:** Is a leading open-source, rule-based Network Intrusion Detection and Prevention System (NIDS/NIPS). It performs real-time traffic analysis and packet logging to detect and prevent malicious network activity and cyber threats.
> 
![](Attachments/Pasted%20image%2020260922022131.png)

**Snort has the following three main use modes ?**
- **Sniffer Mode**: Read and prompt IP packets in the console application.
- **Packet Logger Mode**: Log all IP packets (inbound and outbound) that visit the network.
- **NIDS (Network Intrusion Detection System)  and NIPS (Network Intrusion Prevention System) Modes**: Log/drop the packets deemed malicious according to the user-defined rules.

>==**Snort has three primary uses ??**==
> 1. Packet Sniffer Mode >Snort acts as a real-time network traffic monitor (similar to Wireshark
> 2. Packet Logger Mode >Snort captures network traffic and logs (saves) the packet data to the disk in a specific directory. The logs are typically saved in binary format (such as `.pcap`), which can be analyzed later using tools like Wireshark.
>  3. Network Intrusion Detection & Prevention System (NIDS / NIPS) > 
- **As an IPS (Inline Mode):** It goes a step further by actively dropping malicious packets and blocking the connection to prevent the attack from succeeding.
-  **As an IDS:** It inspects the traffic and generates security alerts (Alerts) when a rule matches a threat.
>


## introduction to IDS/IPS
***A-  Intrusion Detection System (IDS)** = is a passive monitoring solution for detecting possible malicious activities/patterns, abnormal incidents, and policy violations. It generates alerts for each suspicious event.
*  > ==*Type of (IDS)*== ?
   -1Network Intrusion Detection System (NIDS)**: NIDS monitors the traffic flow from various areas of the network. The aim is to investigate the traffic on the entire subnet. If a signature is identified, an alert is created.
   -2 - **Host-based Intrusion Detection System (HIDS)**: HIDS monitors the traffic flow from a single endpoint device. Its aim is to investigate the traffic on that device. If a signature is identified, an alert is created.
   ***B- ## Intrusion Prevention System (IPS)** 
   s an active protecting solution for preventing possible malicious activities/patterns, abnormal incidents, and policy violations. It is responsible for stopping/preventing/terminating the suspicious event as soon as it is detected.
 **There are four main types of IPS systems . ?
 1. Network Intrusion Prevention System (NIPS)**: NIPS monitors the traffic flow from various areas of the network. The aim is to protect the traffic on the entire subnet. If a signature is identified, the connection is terminated.
 2.  Network Behaviour Analysis (NBA)**OR (baselining)Behaviour-based systems monitor the traffic flow from various areas of the network. The aim is to protect the traffic on the entire subnet. If an anomaly is identified, the connection is terminated.
 3. - **Wireless Intrusion Prevention System (WIPS)**: WIPS monitors the traffic flow from a wireless network. Its aim is to protect wireless traffic and stop possible attacks launched from there. If a signature is identified, the connection is terminated.
 4. - **Host-based Intrusion Prevention System (HIPS)**: HIPS actively protects the traffic flow from a single endpoint device. The aim is to investigate the traffic on a particular device. If a signature is identified, the connection is terminated


   - **steps to run snort after installed it ?**
   - 1 make sure of your version by write (snort -V)
   - you should ensure configuration file is valid and identifiese configuration file  by write (sudo snort -c /etc/snort/snort.conf -T) ![](Attachments/Pasted%20image%2020260922022144.png)
   
   
   
   ==**1.Let's run Snort in Sniffer Mode.**== 
   
   As a tool for capturing and analyzing data packets
   ![](Attachments/Pasted%20image%2020260922022158.png)
    **==the most command in this Mode ?==**
|**`-i`**|Specifies the target network interface to sniff.|`sudo snort -v -i eth0`|
|**`-v`**|**Verbose Mode:**     Displays basic network layer headers (IPs, Ports, Protocols).|`sudo snort -v`|
|**`-d`**|**Payload Data:**       Displays the packet application payload (data content).|`sudo snort -d`|
|**`-e`**|**Link-Layer Headers:**    Displays MAC addresses and data-link details.|`sudo snort -de`|
|**`-X`**|**Full Packet Dump:**       Displays full packet details including headers and payload in HEX and ASCII.|`sudo snort -X`|
-- Parameters can be combined either together (`sudo snort -vde`) or separated ( `sudo snort -v -d -e`).

==**2. Let's run Snort in Logger Mode
**==  the most commands in this mode are ?
- -l.  == to   save the loges in current file or directory  with  PCAP Binary file  and with small size  >> sudo snort -dev -l.
- -K ASCII == to show the log packet in ASCII format.   >> sudo snort -dev -K ASCII -l.
- -r  == to read the log packetes from any file 
- -n == with count number of packet 
-  **Note that** Snort can read and handle binary log output (tcpdump and Wireshark can also handle this log format). However, if you create logs with the "-K ASCII" parameter, Snort will not read them.
![](Attachments/Pasted%20image%2020260922022213.png)
#### . File Ownership & Permissions

- **Concept:** Snort requires `root` privileges to sniff traffic (`sudo snort`). Consequently, generated log files are owned by `root`.
- **Fix:** To analyze logs as a regular user without `sudo`, change the file/directory ownership using:
    ```
    sudo chown $USER filename

    sudo chown -R $USER directory_name
    ```
 
 **==what is the BPF ?  ==**
 **Quick Note: Berkeley Packet Filter (BPF)** A kernel-level technology used to filter network traffic efficiently before it reaches user-space applications like Snort. and select the important traffic  or interesting ip or user 

<font color="#00b050">sudo snort -r snort.log.1638459842 icmp -n 10</font>

### **==Snort in IDS/IPS Mode==**
![](Attachments/Pasted%20image%2020260922022219.png)



it shoud  to be 

