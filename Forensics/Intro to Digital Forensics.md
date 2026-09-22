digital forensics is the application of computer science to investigate digital evidence for a legal purpose. Digital forensics is used in two types of investigations:

1. **Public-sector investigations** refer to the investigations carried out by government and law enforcement agencies. They would be part of a crime or civil investigation.
2. **Private-sector investigations** refer to the investigations carried out by corporate bodies by assigning a private investigator, whether in-house or outsourced. They are triggered by corporate policy violations.

### What should you do as a digital forensics investigator? After getting the proper legal authorization ?
1.  Acquire the evidence: Collect the digital devices such as laptops, storage devices, and digital cameras. (Note that laptops and computers require special handling if they are turned on; 
2. Establish a chain of custody: Fill out the related form appropriately
3. 1. Place the evidence in a secure container: You want to ensure that the evidence does not get damaged. In the case of smartphones, you want to ensure that they cannot access the network, so they don’t get wiped remotely.
4. Transport the evidence to your digital forensics lab.
### at your lab the process goes as follows: 
1. 1. Retrieve the digital evidence from the secure container.
2. Create a forensic copy of the evidence: The forensic copy requires advanced software to avoid modifying the original data.
3. Return the digital evidence to the secure container: You will be working on the copy. If you damage the copy, you can always create a new one.
4. Start processing the copy on your forensics workstation.

### What is the Fundamental Principles and Concepts of Digital Investigation ?
- Proper search authority: Investigators cannot commence without the proper legal authority.
- Chain of custody: This is necessary to keep track of who was holding the evidence at any time.
Any person not related to the investigation must not possess the evidence, or it will contaminate the chain of custody of the evidence. A contaminated chain of custody 
- Validation with mathematics: Using a special kind of mathematical function, called a hash function, we can confirm that a file has not been modified.
- Use of validated tools: The tools used in digital forensics should be validated to ensure that they work correctly. For example, if you are creating an image of a disk, you want to ensure that the forensic image is identical to the data on the disk.
- Repeatability: The findings of digital forensics can be reproduced as long as the proper skills and tools are available.
- Reporting: The digital forensics investigation is concluded with a report that shows the evidence related



___
___

## DFIR Tools
#### 1. Eric Zimmerman's tools: >> Artifact Analysis   many 
is a security researcher who has written a few tools to help perform forensic analysis on the Windows platform
#### 2.KAPE: (  Kroll Artifact Parser and Extractor) >> Evidence Collector / Triage
This tool automates the collection and parsing of forensic artifacts and can help create a timeline of events
#### 3.Autopsy: >>Disk Image
Autopsy is an open-source forensics platform that helps analyze data from digital media like mobile devices, hard drives, and removable drives. Various plugins for autopsy speed up the forensic process and extract and present valuable information from the raw data sources.

#### 4. Volatility
 is a tool that helps perform memory analysis for memory captures from both Windows and Linux Operating Systems. It is a powerful tool that can help extract valuable information from the memory of a machine under investigation


#### 5. Redline
is an incident response tool developed and freely distributed by FireEye. This tool can gather forensic data from a system and help with collected forensic information.   ... old 

#### 6. Velociraptor >> Advanced   with Agents 
Velociraptor is an advanced endpoint-monitoring, forensics, and response platform. It is open-source but very powerful.

#### 7 .  AppCompatCacheParser.exe
This tool specializes in extracting and analyzing AppCompatCache/ShimCache.