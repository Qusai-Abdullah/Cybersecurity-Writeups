an open-source generic signature language used to write detection rules applicable across different SIEM backends.

if you write Detection rules  in Splunk you cant reuse it in the sentinel or Elastic The Sigma rules come to solve this problem 🙌 
**Sigma is for log files as Snort is for network traffic, and Yara is for files."**


<mark style="background: #FF5582A6;">Sigma was developed to satisfy the following uses:</mark> ?

- To make detection methods and signatures shareable alongside IOCs and Yara rules.
- To write SIEM searches that avoid vendor lock-in.
- To share signatures with threat intelligence communities.
- To write custom detection rules for malicious behaviour based on specific conditions.

<mark style="background: #FF5582A6;">As a SOC analyst, the process of using Sigma to write up your detection rules will involve understanding the elements mentioned below ?</mark>

- **Sigma Rule Format:** Generic structured log descriptions written in YAML.
- **Sigma Converter:** A set of python scripts that will process the rules on the backend and perform custom field matching based on specified SIEM query language.
- **Machine Query:** Resulting search query to filter out alerts during investigations. The query will be based on the specified SIEM.
- ![](Attachments/Pasted%20image%2020260901175939.png)


<mark style="background: #FF5582A6;">1. what are the step for use sigma >>> </mark>
	* complete write the Detection rules with Sigma formate 
	* convert all rules to be usable in SIEM Tools 
	* Try or appley usable rules in SIEM 






 2.  ### Sigma Syntax ?

- **Title:** Names the rule based on what it is supposed to detect. This should be short and clear.
    
- **ID:** A globally unique identifier mainly used by the developers of Sigma to maintain the order of identification for the rules submitted to the public repository, found in UUID format. 
    
    You may also add references to related rule IDs using the _related_ attribute, making it easier to form relationships between detections. These relations would fall under the following types:
    
    - Derived: This will describe that the rule has sprung from another rule, which may still be active.
    - Obsolete: This will indicate that the listed rule is no longer being used.
    - Merged: This will indicate that the rule combines linked rules.
    - Renamed: This indicates the rule was previously identified under a different ID but has now been changed due to changes in naming schemes or avoiding collisions. 
    - Similar: This attribute points to corresponding rules, such as indicating the same detection content applied to different log sources.

  

- **Status:** Describes the stage in which the rule maturity is at while in use. There are five declared statuses that you can use:  
    

- _Stable_: The rule may be used in production environments and dashboards.
- _Test_: Trials are being done to the rule and could require fine-tuning.
- _Experimental_: The rule is very generic and is being tested. It could lead to false results, be noisy, and identify interesting events.
- _Deprecated_: The rule has been replaced and would no longer yield accurate results. The`related` field is used to create associations between the current rule and one that has been deprecated.
- _Unsupported_: The rule is not usable in its current state (unique correlation log, homemade fields).

  

- **Description:** Provides more context about the rule and its intended purpose. With the rule, you can be as verbose as possible on the malicious activity you intend to detect.  

```shell-session
title: WMI Event Subscription
id: 0f06a3a5-6a09-413f-8743-e6cf35561297
status: test
description: Detects creation of WMI event subscription persistence method.
```

- **Logsource:** 
- Describes the log data to be used for the detection. It consists of other optional attributes:  
    
    - _Product_: Selects all log outputs of a particular product. Examples are Windows, Apache.
    - _Category_: Selects the log files written by the selected product. Examples are firewall, web, and antivirus.
    - _Service_: Selects only a subset of the logs from the selected product. Examples are _sshd_ on Linux or _Security_ on Windows.
    - _Definition_: Describes the log source and any applied configurations.

```shell-session
logsource:
   product: windows    
   category: wmi_event 
      
```

- **Detection:** A required field in the detection rule describes the parameters of the malicious activity we need an alert for. The parameters are divided into two main parts: the search identifiers - the fields and values that the detection should be searching for -  and condition expression - which sets the action to be taken on the detection, such as selection or filtering. More on this is below.    <(what are The things we are looking for  ?)>
- 
- This rule has a detection modifier that looks for logs with one of Windows Event IDs 19, 20 or 21. The condition informs the detection engine to match and select the identified logs.

```shell-session
detection:
  selection:   £ It is the part that identifies the behavior you want to discover.
    EventID:  # This shows the search identifier value
      - 19    # This shows the search's list value
      - 20
      - 21
  condition: selection
```
 Example with tow conditions

```
detection:
   selection:
   Image: powershell
   CommandLine: '-hidden'
   
```

another Example with (AND   ,   OR , contains , all )

```
selection:
   CommandLine|contains: # that mean if the commandline contains <-enc> anywhere
   - '-enc'
     
   2  (contains with all) Examle(2)
   selection:
	   CommandLine|contains|all: # the commandline must contains tow prameter
   - '-net'
    - '-user' 
   3
   selection:
    CommandLine|contains|any: any one should be true 
        - '-enc'
        - '-encodedcommand'
     
     
     
```

<mark style="background: #FF5582A6;"> *<u>Multiple Selections</u>* ?
</mark> ```
```
detection:
   user_creation:
   EvintID: 4720
   
   suspicous_user:User|contains:
   - admin
    - test
      
condition: user_creation and suspious_user 
```


- **FalsePositives:** A list of known false positive outputs based on log data that may occur.
    
- **Level:** Describes the severity with which the activity should be taken under the written rule. The attribute comprises five levels: Informational -> Low -> Medium -> High -> Critical
    
- **Tags:** Adds information that may be used to categorise the rule. Tags may include values for CVE numbers and tactics and techniques from the MITRE ATT&CK framework. Sigma developers have defined a list of [predefined tags(opens in new tab)](https://github.com/SigmaHQ/sigma/wiki/Tags).
    

WMI_Event_Subscription.yml

```shell-session
falsepositives:
    - Exclude legitimate (vetted) use of WMI event subscription in your network

level: medium

tags:
  - attack.persistence # Points to the MITRE tactic.
  - attack.t1546.003   # Points to the MITRE technique.      
       
```

### Search Identifiers and Condition Expressions

As mentioned earlier, the detection section of the rule describes what you intend to search for within the log data and how the selection and filters are to be evaluated. The definition of the search identifiers can comprise two data structures - **lists and maps** - which dictate the order in which the detection would be processed.

When the identifiers are provided using lists, they will be presented using strings linked with a logical **'OR'** operation. Mainly, they will be listed using hyphens (-). For example, below, we can look at an extract of the [Netcat Powershell Version rule(opens in new tab)](https://github.com/SigmaHQ/sigma/blob/master/rules/windows/powershell/powershell_classic/posh_pc_powercat.yml) where the detection is written to match on the `HostApplication` field containing 'powercat' or 'powercat.ps1' as its value.

Posh_PC_Powercat.yml

```shell-session
detection:
  selection:
    HostApplication|contains:
         - 'powercat'
         - 'powercat.ps1'
  condition: selection     
      

On the other hand, maps comprise key/value pairs where the key matches up to a field in the log data while the value presented is a string or numeral value to be searched for within the log. Maps follow a logical **'AND'** operation.

As an example, we can look at the [Clear Linux log rule(opens in new tab)](https://github.com/SigmaHQ/sigma/blob/master/rules/linux/process_creation/proc_creation_lnx_clear_logs.yml) where the `selection` term forms the map, and the rule intends to match on `Image|endswith` either of the values listed, AND `CommandLine` contains either value listed. This example shows how maps and lists can be used together when developing detections. It should be noted that `endswith` and `contains` are value modifiers, and two lists are used for the search values, where one of each group has to match for the rule to initiate an alert. 

Process_Creation_Lnx_Clear_Logs.yml

shell-session
detection:
  selection:
    Image|endswith:
         - '/rm' # covers /rmdir as well
         - '/shred'
    CommandLine|contains:
         - '/var/log'
         - '/var/spool/mail'
  condition: selection

As we have mentioned the value modifier, it is worth noting that they are appended after the field name with a pipe character (|), and there are two types of value modifiers:

- **Transformation modifiers:** These change the values provided into different values and can modify the logical operations between values. They include:
    
    - _contains:_ The value would be matched anywhere in the field.
    - _all:_ This changes the OR operation of lists into an AND operation. This means that the search conditions has to match all listed values.
    - _base64:_ This looks at values encoded with Base64.
    - _endswith:_ With this modifier, the value is expected to be at the end of the field. For example, this is representative of `*\cmd.exe`.
    - _startswith:_ This modifier will match the value at the beginning of the field. For example, `power*`.
- **Type modifiers:** These change the type of the value or sometimes even the value itself. Currently, the only usable type modifier is `re`, which is supported by Elasticsearch queries to handle the value as a regular expression.

For conditions, this is based on the names set for your detections, such as _selection and_ _filter,_ and will determine the specification of the rule based on a selected expression. Some of the terms supported include:

- **Logical AND/OR**
- **1/all of search-identifier**
- **1/all of them**
- **not**

An example of these conditional values can be seen in the extract below from the [Remote File Copy rule(opens in new tab)](https://github.com/SigmaHQ/sigma/blob/master/rules/linux/builtin/lnx_file_copy.yml), where the detection seeks to look for either of the tools: `scp`, `rsync` or `sftp` and with either filter values `@` or `:`.

Remote_File_Copy.yml

shell-session
detection:
  tools:
         - 'scp'
         - 'rsync'
         - 'sftp'
  filter:
         - '@'
         - ':'
  condition: tools and filter

Another example to showcase a combination of the conditional expressions can be seen in the extract below from the [Run Once Persistence Registry Event rule(opens in new tab)](https://github.com/SigmaHQ/sigma/blob/master/rules/windows/registry/registry_event/registry_event_runonce_persistence.yml), where the detection seeks to look for values on the map that start and end with various registry values while filtering out Google Chrome and Microsoft Edge entries that would raise false positive alerts.

Registry_Event_RunOnce_Persistence.yml

shell-session
detection:
  selection:
    TargetObject|startswith: 'HKLM\SOFTWARE\Microsoft\Active Setup\Installed Components'
    TargetObject|endswith: '\StubPath'
  filter_chrome:
    Details|startswith: '"C:\Program Files\Google\Chrome\Application\'
    Details|endswith: '\Installer\chrmstp.exe" --configure-user-settings --verbose-logging --system-level'
  filter_edge:
    Details|startswith:
    - '"C:\Program Files (x86)\Microsoft\Edge\Application\'
    - '"C:\Program Files\Microsoft\Edge\Application\'
    Details|endswith: '\Installer\setup.exe" --configure-user-settings --verbose-logging --system-level --msedge 
    --channel=stable'
  condition: selection and not 1 of filter_*

<mark style="background: #FF5582A6;">  3. what are Common factors to note about YAML files are:?</mark>
  - YAML is case-sensitive.
- Files should have the `.yml` extension.
- Spaces are used for indentation and not tabs.
- Comments are attributed using the `#` character.
- Key-value pairs are denoted using the colon `:` character.
- Array elements are denoted using the dash `-` character.

```


<mark style="background: #FF5582A6;"> ***NOW We will make full Scenario ..***</mark>

. Administrators rely on remote tools to ensure devices are configured, patched and maintained. However, your SOC Manager just received and shared intel on how AnyDesk, a legitimate remote tool, can be downloaded and installed silently on a user's machine using the file description on the right-hand side. (Source: [TheDFIRReport(opens in new tab)](https://twitter.com/TheDFIRReport/status/1423361127472377860?s=20&t=mHiJFnlfWH3cO3XdXEQo_Q)). As a SOC analyst, you have been tasked to analyse the intel and write a Sigma rule to detect the installation of AnyDesk on Windows devices.
. ![](Attachments/Pasted%20image%2020260712003950.png)

#### Step 1: Intel Analysis

The shared intel shows us a lot of information and commands to download and install AnyDesk. An adversary could wrap this up in a malicious executable sent to an unsuspecting user through a phishing email. We can start picking out values that would be important for detecting any occurrence of an installation.

- Source URL: This marks the download source for the software, highlighted by the $url variable.
- Destination File: The adversary would seek to identify a destination directory for the download. This is marked by the $file variable.
- Installation Command: From the intel, we can see that various instances of `CMD.exe` are being used to install and set a user password by the script. From this, we can pick out the installation attributes such as `--install`, `--start-with-win` and `--silent`.

Other essential pieces of information from the intel would include:

- Adversary Persistence: The adversary would seek to maintain access to the victim's machine. In this instance, they would create a user account `oldadministrator` and give the user elevated privileges to run other tasks.
- Registry Edit: We can also pick out the registry edit, where the added user is added to a `SpecialAccounts` user list.

With this information, we can evaluate the creation of a rule to aid in detecting when an installation has taken place.
#### Step 2: Rule Identification

We can start building our rule by filling in the Title and Description sections, given the information that we are looking for an AnyDesk remote tool installation. Let us also set the status as `experimental` , as this rule will be tested internally.

title: AnyDesk installation
status: Experimental
description: AnyDesk Remote Desktop installation can by used by attacker  to gain remote access 


#### Step 3: Log Source
As indicated from our intel, Windows devices would be our targetted device

loogsource:
   category: process_creation
   product: windows

#### Step 4: Detection Description
The detection section of our rule is the essential part. here in this part we will define what we need to detect within our environment 
```
detection:
	selection:
		CommandLine|contains:
		- '--install'
		  -'--start-with-win'
		currentDirectory|contains:
			- 'C:programData\AnyDesk.exe'
condition: selection 
```


#### Step 5: Rule Conversion
Sigma rules need to be converted to the appropriate SIEM target that is being utilised to store all the logs. Using the rule we have written above
**now learn how to use the<mark style="background: #D2B3FFA6;"> sigmac</mark> and <mark style="background: #D2B3FFA6;">uncoder.io</mark> tools to convert them into ElasticSearch and Splunk queries.**

## What is The Sigmac ?
 is a Python-written tool that converts Sigma rules by matching the detection log source field values to the appropriate SIEM backend fields. As part of the Sigma repo (Advisable to clone the repo to get the tool and all the available rules published by the Sigma team https://github.com/SigmaHQ/sigma/tree/8bb3379b6807610d61d29db1d76f5af4840b8208/tools
  this tool allows for quick and easy conversion of Sigma rules from the command line.
>[!note] 
> Sigmac will be deprecated by the end of 2022, and attention from the owners will shift to sigma-cli.

sudo python3.9 -m pip install ruamel.yaml >> to download important library for yaml file
python3.9 sigmac -h 
![](Attachments/Pasted%20image%2020260712025245.png)
***####The main options to be used are?***
* - -t: This sets the targeted SIEM backend you wish to get queries for (Elasticsearch, Splunk, QRadar, ElastAlert).
* convert to Elasticsearch >>python3.9  sigmac \-t es-qs \rule.yml 
* convert to splunk >>  python3.9 sigmac \-t splunk \rule.yml 
* -c     or  --config >>  sets file Field Mapping Configuration  ! ? This means linking the field names in Sigma with the fields you have in SIEM.
* -o or  --output >> to save result in file 
* --backend-option: This allows you to pass a backend configuration file or individual modifications that dictate alert options for the target SIEM environment. For example, in ElasticSearch, we can specify specific field properties to be our primary keyword_field to be searched against, such as fields that end in the `.keyword` or `.security`  python3.9 sigmac -t es-qs -c tools/config/winlogbeat.yml --backend-option keyword_field=".keyword" --backend-option analyzed_sub_field_name=".security" ../rules/windows/sysmon/sysmon_accessing_winapi_in_powershell_credentials_dumping.yml


***We can convert our AnyDesk Installation rule  to a Splunk alert as shown below:***
```
python3.9 sigmac -t splunk -c splunk-windows Process_Creation_AnyDesk_Installation.yml

```
Sigma developers are working on a Python library that will be Sigmac's replacement, known as [pySigma](https://github.com/SigmaHQ/pySigma)

# Uncoder.io  https://uncoder.io/?
is an online Sigma converter for numerous SIEM and EDR platforms. It is easy to use as it allows you to copy your Sigma rule on the platform and select your preferred backend application for translation. Do take note that with recent updates, this requires setting up a free account on the uncoder.io website.
![](Attachments/Pasted%20image%2020260712032336.png)














>[!The Second  Scenario ]
You want to write a rule to detect the operation of the Windows certificate management and encryption tool certutil.exe (attackers frequently exploit this to download malicious files from the internet using the -urlcache command).
However, your company's IT department uses this tool normally and routinely, but only through an administrator account named IT_Admin. If any other user were to run it, that would be extremely dangerous!

The rule for it >>
```
title: Detects execution certutil tool
id: ca8d91dc-fd16-4c53-980a-32e0cedff9df
status: experimental
description: detects execution malicious  commands or expliot the certtutil tool to download any  malicious file
logsource:
  category: process_creation
  product: windows
detection:
   selection:
      Image|endswith: '\certutil.exe'
      CommandLine|contains: '-urlcache'
    filter:
        User: IT_Admin
    condition: selection and not filter
level: medium
```


>[!The threed  Scenario ]
>An attacker ran the built-in windows tool vssadmin.exe to delete system backup 
>(shadow copies), preventing the victim from recovering their files after they were encrypted by ransomware.
The command the attacker typically writes is: vssadmin.exe delete shadows /all /quiet

 The rule for it  >>
```
title: Detects execution vssadmin tool
id: ca8d91dc-fd16-4c53-980a-32e0cedff9df
status: experimental
description: detects execution vssadmin tool to delete The backup of system
logsource:
  category: process_creation
  product: windows
detection:
   selection:
      Image|endswith: '\vssadmin.exe'
      CommandLine|contains|all:
        - 'delete'
        - 'shadows'
    condition: selection
level: high

```

>[!The fourth scenario  >> (Advansed)] 
>title: Detects Burte force Authentication Failure
id: ca8d91dc-fd16-4c53-980a-32e0cedff9df
status: experimental
description: detects multiple failed lohin attemps indicating a brute force  Attack
logsource:
  service: security
  product: windows
detection:
  selection:
    EventID: 4625
  condition: selection | count(EventID) > 5 by TargetUserName timeframe(1m)
level: high 



>[! the last Scenario (Advansed)]
>In a Windows networking environment (Active Directory), malicious actors "reconnoiter" sensitive groups (such as the Domain Admins group).
If a regular user queries groups rapidly using the net.exe tool (which we practiced), and this is done more than three times within two minutes by the same user, this is a strong indicator of malicious reconnaissance (internal reconnaissance).
>

The rule for it >>
```
title: Detects Attacker Reconnaissance Survey
id: ca8d91dc-fd16-4c53-980a-32e0cedff9df
status: experimental
description: Detects multiple net.exe executions by the same user within a short timeframe, indicating reconnaissance.
logsource:
  category: process_creation
  product: windows
detection:
  selection:
    Image|endswith: '\net.exe'
  condition: selection | count(Image) > 3 by User timeframe(2m)
level: high



```

![](Attachments/Pasted%20image%2020260713033706.png)


![](Attachments/Pasted%20image%2020260713033734.png)

![](Attachments/Pasted%20image%2020260713033746.png)







![](Attachments/Pasted%20image%2020260713033652.png)






