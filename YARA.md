YARA is a specialized, open-source pattern-matching and rule-based language used primarily in cybersecurity. It allows analysts and researchers to identify, classify, and detect malware by searching for specific <font color="#f79646">textual</font>, <font color="#f79646">binary</font>, or <font color="#f79646">hexadecimal</font> patterns within
for EX: the code below  prints "Hello World" in Python. The text "Hello World" would be stored as a string.
```python
print("Hello World!")
```
We could write a Yara rule to search for "hello world" in every program on our operating system if we would like.  
rule is only as effective as your understanding of the patterns you want to search for.
 Every `yara` command requires two arguments to be valid, these are:  
**1)** The rule file we create  
**2)** Name of file, directory, or process ID to use the rule for.
for EX : `yara myrule.yar somedirectory`
Note that **.yar** is the standard file extension for all Yara rules

1. some useful commands
	* yara myfirstrule.yar suspicious-files/file1 >>  to check the specific file 
	* yara myfirstrule.yar -r suspicious-files/    >>  to check full folder 


![](Attachments/Pasted%20image%2020260705021216.png)






2. We can apply Yara to anything that contains digital bits like ....?
* .  file  with any Extension below  >>>  exe , elf , rar , zip  or any type of picture
* Processes / RAM  in memory 
* folders
* ![](Attachments/Pasted%20image%2020260705022418.png)
2. 
![](Attachments/Pasted%20image%2020260705022525.png)

<mark style="background: #FF5582A6;"> ** Some Keyword**
</mark> 
<mark style="background: #FFF3A3A6;">|Desc >></mark> This section of a Yara rule is reserved for descriptive information by the author of the rule. For example, you can use `desc`, short for description, to summarise what your rule checks for.
<mark style="background: #FFF3A3A6;">|Meta>></mark> 
<mark style="background: #FFF3A3A6;">|Strings >></mark> You can use strings to search for specific text or hexadecimal in files or programs
```yaml
rule helloworld_checker{
	strings:
		$hello_world = "Hello World!"
}
```
<mark style="background: #FFF3A3A6;">|Conditions>></mark>  we need a condition here to make the rule valid. In this example, to make this string the condition, we need to use the variable's name. In this case, `$hello_world`:

```yaml
rule helloworld_checker{
	strings:
		$hello_world = "Hello World!"

	condition:
		$hello_world
}
```
 
 
 if any file has the string "Hello World!" then the rule will match. However, this is literally saying that it will only match if "Hello World!" is found and will not match if "_hello world_" or "_HELLO WORLD_."  *<u>To solve this >>></u>  the condition `any of them` allows multiple strings to be searched for* EX : 
```yaml
 yaml
rule helloworld_checker{
	strings:
		$hello_world = "Hello World!"
		$hello_world_lowercase = "hello world"
		$hello_world_uppercase = "HELLO WORLD"

	condition:
		any of them
}
}
```
Now, any file with the strings of:
1. Hello World!
2. hello world
3. HELLO WORLD
<mark style="background: #FF5582A6;"><u> you can use operators such  ?:</u></mark>
- **<=** (less than or equal to)
- **>=** (more than or equal to)
- **!=** (not equal to)
For example, the rule below would do the following:

```yaml
rule helloworld_checker{
	strings:
		$hello_world = "Hello World!"

	condition:
        #hello_world <= 10
}
```
The rule will now:
1. Look for the "Hello World!" string  
2. Only say the rule matches if there are less than or equal to ten occurrences of the "Hello World!" string


<mark style="background: #FF5582A6;">Combining keywords
</mark> 
Moreover, you can use keywords such as:
- and
- not
- or
To combine multiple conditions. Say if you wanted to check if a file has a string and is of a certain size (in this example, the sample file we are checking is **less than** <10 kb and has "Hello World!" you can use a rule like below:  
```yaml
rule helloworld_checker{
	strings:
		$hello_world = "Hello World!" 
        
        condition:
	        $hello_world and filesize < 10KB 
}
```
The rule will only match if both conditions are true. 


![](Attachments/Pasted%20image%2020260705231914.png)

> [!note]  some of 
>1.You can add comments to your YARA rules by /*   */ .
>2. Text strings in YARA are case-sensitive by default  to solve it you can use ( no case  )
>3. Wide-character strings  The `wide` modifier can be used to search for strings encoded with two bytes per character, something typical in many executable binaries. For example, if the string "Borland" appears encoded as two bytes per character (`B\x00o\x00r\x00l\x00a\x00n\x00d\x00`), then the following rule will match 
>4. incomplete
> :

>[!tip]   Best practice 
>1. use  ==**(Cuckoo== )** Cuckoo Sandbox is an automated malware analysis environment. This module allows you to generate Yara rules based upon the behaviours discovered from Cuckoo Sandbox. As this environment executes malware, you can create rules on specific behaviours such as runtime strings and the like.
>2. use   ==(Python PE ) **==   Python's PE module allows you to create Yara rules from the various sections and elements of the Windows Portable Executable (PE) structure.
>3. use the (VMRay) its use Hypervisor-based analysis its mean the malware cant konw your environment 
>4. use (==ANY.RUN)==   (Live Interaction) You can see all the virus movements

Knowing how to create custom Yara rules is useful, but luckily you don't have to create many rules from scratch to begin using Yara to search for evil. There are plenty of GitHub [resources](https://github.com/InQuest/awesome-yara)
 and open-source tools (along with commercial products) that can be utilized to leverage Yara in hunt operations and/or incident response engagements.
 There are additional checks that LOKI can be used for. For a full rundown, please reference the [GitHub readme](https://github.com/Neo23x0/Loki/blob/master/README.md)
 LOKI can be used on both Windows and Linux systems and can be downloaded [here](https://github.com/Neo23x0/Loki/releases)
>[!important]  YARA Tools ?
>1.<mark style="background: #FF5582A6;"> LOKI  >></mark> LOKI is a free open-source IOC (_Indicator of Compromise_) scanner created/written by Florian Roth.
Based on the GitHub page, detection is based on 4 methods 
.File Name IOC Check
.Yara Rule Check 
 . Hash Check 
 . C2 Back Connect Check
>2.  <mark style="background: #FF5582A6;">YARA >></mark> YAYA was created by the [EFF(opens in new tab)](https://www.eff.org/deeplinks/2020/09/introducing-yaya-new-threat-hunting-tool-eff-threat-lab) (_Electronic Frontier Foundation_) and released in September 2020. Based on their website, "_YAYA is a new open-source tool to help researchers manage multiple_
>_YARA rule repositories. YAYA starts by importing a set of high-quality YARA rules and then lets researchers add their own rules, disable specific rulesets, and run scans of files_
>Note: Currently, YAYA will only run on Linux systems.
>3.<mark style="background: #FF5582A6;"> THOR Scanner >></mark>   (_superhero named programs for a superhero blue teamer)_
>THOR _Lite_ is Florian's newest multi-platform IOC AND YARA scanner. There are precompiled versions for Windows, Linux, and macOS. A nice feature with THOR Lite is its scan throttling to limit exhausting CPU resources. For more information and/or to download the binary, start [here](https://www.nextron-systems.com/thor-lite/) or visit (Nextron Systems)  You need to subscribe to their mailing list to obtain a copy of the binary. **Note that THOR is geared towards corporate customers**. THOR Lite is the free version.
. 4<mark style="background: #FF5582A6;">FENRIR >></mark>
>.5 EDR (Endpoint Detection and Response) >>

We will practice LOKI  ?
1. python3 loki.py -p . >>_(النقطة `.` تعني فحص المجلد الحالي الذي تقف فيه)._
2.  python /home/cmnatic/tools/Loki/loki.py -p.
3. ![](Attachments/Pasted%20image%2020260708000909.png)What are the important pieces of information from the outputs?
* .Does Loki detect this file as suspicious/malicious or benign >> Suspicious
* What Yara rule did it match on >> webshell_metaslsoft
* What does Loki classify this file as >> Web Shell
* Based on the output, what string within the Yara rule did it match on >> Str1
* What is the name and version of this hack tool >>b374k 2.2

	


>[!tip] If you will making rule for any Detection you must  ask  some of Question that  are ..... ?
>4. what are the things that's cant be easily changed  in this program  like protocol or  Communication Transports  ?
>5. Ask yourself if the signatures that were collected are unique
>6. analysis this program with IDA OR Ghidra OR Debb






***<mark style="background: #FF5582A6;"> what is arGen ..?</mark>***
 yarGen is a generator for YARA rules.
 An automated security tool used by cyber analysts to **generate YARA rules (malware detection signatures) automatically**. It analyzes malware samples, extracts unique indicators, and writes the rules instantly to help security systems and SOC teams detect digital threats.

### **Benefits of yarGen:**

- **Time-Saving & Automation:** It creates detection rules in seconds instead of hours of manual analysis.
- **Low False Positives:** It filters out common strings using a massive built-in "Goodware" database, ensuring clean system files are not accidentally flagged or blocked.
- **Rapid Incident Response:** It allows SOC and Incident Response teams to quickly deploy custom signatures to block active or newly discovered zero-day attacks.
- **Smart Indicator Extraction:** It automatically combines unique string signatures and Hex opcodes for high-accuracy threat hunting.
How use its  or what are commands for use it ?
1.<mark style="background: #FFB8EBA6;"> python yarGen.py --update</mark>  >> for update 
1. <mark style="background: #FFB8EBA6;">python yarGen.py -m /path/to/malware -o my_rules.yar </mark>  >> for examining  specific folder
			-m  for set the file you want to analysis it  and -o that is for save output 
2. in the below we try to doing the commandds 
3. ![](Attachments/Pasted%20image%2020260708164706.png)
	1. ![](Attachments/Pasted%20image%2020260708164948.png)  In the picture above, it shows where the rules were saved.




 ]]*. From within the root of the suspicious files directory, what command would you run to test Yara 
 and your Yara rule against file 2? 
yara file2.yar file2/1ndex.php


 mv qusai.yra /home/cmnatic/tools/Loki/signature-base



**Valhalla** ? https://www.nextron-systems.com/valhalla/
![](Attachments/Pasted%20image%2020260709032145.png)





## Conclusion

Yara rules are extremely valuable for malware analysis and detection. File 2 was not detected in the open-source version of Loki. This demonstrates the need to use more than just one resource for malware analysis along with investing in valuable commercial products as well because the Yara rule is available in Loki’s commercial variant called Thor.









