### A) what is the NTFS ?
NTFS is known as a journaling file system. In case of a failure, the file system can automatically repair the folders/files on disk using information stored in a log file. This function is not possible with FAT.

#### Let's speak briefly on some features that are specific to NTFS.
1. **permissions  ** >> 
2. **Alternate Data Streams** It is an NTFS feature that allows a file to contain more than one data stream. >> test.txt
   |
   └── $DATA

Alternate Data Streams (ADS) have been given a bad reputation because their capability to hide data from us on our own computer, has been abused by malware writers in the past. Hopefully this article will clear up some of the questions and mystique you had about ADS

![](Attachments/Pasted%20image%2020260813034829.png)

### The pertany commands 
```
```:: 1. Create a normal file
echo this the normal data > qusai1.txt

:: 2. Display the normal file content
type qusai1.txt

:: 3. Create an Alternate Data Stream (ADS)
echo This is hidden ADS data > qusai1.txt:secret

:: 4. Display the normal stream
type qusai1.txt

:: 5. Display the ADS content
more < qusai1.txt:secret

:: 6. List the file and its ADS
dir /r qusai1.txt


```

## Why is ADS dangerous? 
Because Windows Explorer does not display ADS to the user in the usual way.

## The difference between the file and the ADS.?

1. C:\test.txt  normal
2. test.txt:hidden   the ADS

___
___
___
### B) The Windows folder ( `C:\Windows`) ?
is traditionally known as the folder which contains the Windows operating system.
The folder doesn't have to reside in the C drive necessarily. It can reside in any other drive and technically can reside in a different folder.
%windir%  to reach into windoes

![](Attachments/Pasted%20image%2020260813040841.png)

# ## One of the many folders is **System32** .
The System32 folder holds the important files that are critical for the operating system.

![](Attachments/Pasted%20image%2020260813041508.png)

___ 
___
___
### C) User Accounts, Profiles, and Permissions ?


### to see All users in windows ?

1. Managing users and local groups >> (lusrmgr.msc)  
2. net user
3. (C:\Users)

___
___
### D )**Task Manager**.
The Task Manager provides information about the applications and processes currently running on the system. Other information is also available, such as how much CPU and RAM are being utilized, which falls under Performance




TO access  into Task Manager ?
1. ![](Attachments/Pasted%20image%2020260814011055.png)
2.   ```
   taskmgr
   ```


## Task Manager's Simple View
![](Attachments/Pasted%20image%2020260814011305.png)
The first time you launch the Task Manager, you'll see a small, simple window. This window lists the visible applications running on your desktop, excluding background applications. You can select an application here and click "End Task" to close it. This is useful if an application isn't responding — in other words, if it's frozen — and you can't close it the usual way.
## You can also right-click an application in this window to access more options:
- **Switch To**: Switch to the application's window, bringing it to the front of your desktop and putting it in focus. This is useful if you're not sure which window is associated with which application.
- **End Task**: End the process. This works the same as the "End Task" button.
- **Run New Task**: Open the Create New Task window, where you can specify a program, folder, document, or website address and Windows will open it.
- **Always On Top**: Make the Task Manager window itself "always on top" of other windows on your desktop, letting you see it at all times.
- **Open File Location**: Open a File Explorer window showing the location of the program's .exe file.
- **Search Online**: Perform a Bing search for the program's application name and file name. This will help you see exactly what the program is and what it does.
- **Properties**: Open the Properties window for the program's .exe file. Here you can tweak compatibility options and see the program's version number, for example.


## Controlling Startup Applications
![](Attachments/Pasted%20image%2020260814013606.png)

## Checking on Users
![](Attachments/Pasted%20image%2020260814013639.png)

## Working With Services
![](Attachments/Pasted%20image%2020260814013917.png)
The Services tab shows a list of the system services on your Windows system. These are background tasks that Windows runs, even when no user account is signed in. They're controlled by the Windows operating system. Depending on the service, it may be automatically started at boot or only when necessary.

Many services are part of Windows 10 itself. For example, the Windows Update service downloads updates and the Windows Audio service is responsible for sound. Other services are installed by third-party programs. For example, [NVIDIA installs several services](https://www.howtogeek.com/343120/what-are-all-those-nvidia-processes-running-in-the-background/) as part of its graphics drivers.

You shouldn't mess with these services unless you know what you're doing. But, if you right-click them, you'll see options to Start, Stop, or Restart the service. You can also select Search Online to perform a Bing search for information about the service online or "Go to Details" to show the process associated with a running service on the Details tab. Many services will have a "[svchost.exe](https://www.howtogeek.com/987/what-is-svchostexe-and-why-is-it-running/)" process associated with them.

The Service pane's columns are:

- **Name**: A short name associated with the service
- **PID**: The process identifier number of the process associated with the service.
- **Description**: A longer name that provides more information about what the service does.
- **Status**: Whether the service is "Stopped" or "Running."
- **Group**: The group the service is in, if applicable. Windows loads one service group at a time at startup. A service group is a collection of similar services that are loaded as a group.



## Process Explorer: A More Powerful Task Manager
![](Attachments/Pasted%20image%2020260814014045.png)

ended  The module .
##### In future modules, we'll cover topics like the Windows folder, the management console, security tools (Windows Defender, Windows Firewall, etc.), to name a few.
___
___
___
### The  future come now ..

# Windows Fundamentals 2
This module will attempt to provide an overview of some other utilities available within the Windows operating system and different methods to access these utilities.


### 1. System Configuration 
utility (`MSConfig`) is for advanced troubleshooting, and its main purpose is to help diagnose startup issues.  O R its Managing Windows startup and troubleshooting boot issues.


ex in arabic 
```
إذا شعرت يوماً أن جهازك يبدأ التشغيل ببطء، أو هناك برنامج خبيث/مزعج يفتح تلقائياً مع تشغيل الكمبيوتر ولا تعرف كيف تغلقه، فإن **MSConfig** هي "الورشة السريعة" التي تدخل إليها لتحديد ما يسمح له بالعمل وما يُمنع!
```
###### There are several methods to launch System Configuration. One method is from the 
Start Menu.
![](Attachments/Pasted%20image%2020260814020932.png)

The utility has five tabs across the top. Below are the names for each tab. We will briefly cover each tab in this task. 

## 1)General
![](Attachments/Pasted%20image%2020260814033307.png)
- **Normal startup**  >> This is the normal situation. 
- **Diagnostic startup** >> It is similar to running Windows in diagnostic mode, where a limited set of essential components is loaded.
- **Selective startup** >> You can specify what gets loaded.
## 2)Boot
**Boot Configuration Data** BCD  >> It is a settings store used by Windows Boot Manager to determine how and where Windows boots.
![](Attachments/Pasted%20image%2020260814033851.png)
## 3)Services >>
Service is a background process that can start: At
* boot
* Upon login
* When a specific service is requested
![](Attachments/Pasted%20image%2020260814034340.png)
## 4)Startup
In recent versions of Windows (Windows 10 and Windows 11), the management of programs that run automatically at startup has been moved from this tool to the Task Manager.
![](Attachments/Pasted%20image%2020260814035058.png)

![](Attachments/Pasted%20image%2020260814035114.png)

### The important Startup Folder location is .... ?
```
shell:common startup
shell:startup
HKCU\Software\Microsoft\Windows\CurrentVersion\Run
HKLM\Software\Microsoft\Windows\CurrentVersion\Run

```


## 5)Tools >> 
These tools are your eye on what's happening inside the system.
![](Attachments/Pasted%20image%2020260814041355.png)

<mark style="background: #FFF3A3A6;">if you need To run any tool just press on the Launch bottom </mark>

___
___

## Advanced System Settings
Windows gives you some additional configuration settings as well, which you can use to control the performance behavior and **system recovery. **

**To access this option**, you can search for 
```
`View advanced system settings` OR  CMD `sysdm.cpl`
```
![](Attachments/Pasted%20image%2020260814043055.png)


***Windows uses a page file as an extra virtual memory space*** when the physical RAM becomes full. This helps to prevent slowdowns or application crashes when the system runs out of memory. You can view or modify the page file by navigating to the `Advanced` option at the top and clicking `Settings` under the `Performance` tab.
___
___


## Advanced System Settings ?
Windows gives you some additional configuration settings as well, which you can use to control the performance behavior and system recovery.

To access this option, you can search for ...?
View advanced system settings

![](Attachments/Pasted%20image%2020260814213303.png)

>[! note] 
>
Windows uses a page file as an extra virtual memory space when the physical RAM becomes full. This helps to prevent slowdowns or application crashes when the system runs out of memory. You can view or modify the page file by navigating to the `Advanced` option at the top and clicking `Settings` under the `Performance` tab.

![](Attachments/Pasted%20image%2020260814221026.png)
So after clicking the Settings, you will get the Performance Options window, as can be seen below:

![](Attachments/Pasted%20image%2020260814221048.png)


There is another cool configuration that you can find in the Advanced System Settings. It is known as Startup and Recovery. Windows can create a crash dump file whenever it encounters a critical error, such as a Blue Screen of Death. This crash dump helps the administrators or analysts understand what went wrong during the crash. You can view or modify the crash dump settings by navigating to the `Advanced` option at the top and then clicking `Settings` under the `Startup and Recovery` section.
![](Attachments/Pasted%20image%2020260814221231.png)
So after clicking the settings, you will see the `Startup and Recovery` window, as shown below:
![](Attachments/Pasted%20image%2020260814221251.png)











### to reduce the time of setup  ?
![371](Attachments/Pasted%20image%2020260814215252.png)

Here, you will find different settings for the startup and recovery. The `Write debugging information` dropdown tells you the type of crash dump configured for the system. Windows supports different dump types, such as:

- Automatic memory dump
- Kernel memory dump
- Small memory dump (256 KB)
- Complete memory dump
- None
 **This setting shows how much information Windows will save in the crash dump when a system crash occurs.**

### What is the Dual Boot  mean  ?
It's a process that allows you to install two (or more) different operating systems on the same computer, with the option to choose between them each time you start the computer.


useful command 
for see the version of system , number 0f  build  and licensed information's

```
winver
```
### Its main benefits of MSconfig are ?
1.  Speeding up computer startup (Startup):
Allows you to see and control the programs that start automatically when your computer turns on, and stop the heavy ones.
2. Entering "Safe Mode" (Safe Mode): Safe Mode is basically putting Windows into a 'clean state with the least possible resources'; the system only runs the absolute essential services and drivers, without running any third-party programs in the background.
If your device gets a virus or a problem that prevents it from opening normally, you can use the (Boot) tab to set the device to start in "Safe Mode" with one click to fix the issue.
3. Disabling annoying services (Services):
Lets you stop Windows services or external programs that run in the background and use up memory (RAM) and CPU.
4. Running advanced system tools (Tools):
Gathers the most important complex Windows tools into one list so you can open them with a single click instead of searching for them.
___
___
### Change UAC Settings
This slider has four security levels, each of which controls how Windows alerts you when apps or users try to make changes at the system level. They fall into four standard categories as explained below:

- **Always notify:** This is the highest security. Windows notifies you whenever any apps or you yourself try to make changes, and the desktop dims (Secure Desktop).
    
- **Notify for apps**: Windows notifies only when _apps_ try to make changes, but not when you change Windows settings. This option is enabled by default.
    
- **Notify without dimming:** Same as above (Notify for apps), but this time the screen does not dim. 
    
- **Never notify:** Notifications are turned off. Windows won’t warn you about any changes made by you or any apps. 
    

You can find the current level by looking at the position of the slider in the `User Account Control settings` window, as shown below:

![](Attachments/Pasted%20image%2020260815225640.png)


___
___
### Computer Management

**`compmgmt.msc`** to reach into it <<
The **Computer Management** (`compmgmt`) utility has three primary sections: System Tools, Storage, and Services and Applications.
![](Attachments/Pasted%20image%2020260815230014.png)

**System Tools**

Let's start with **Task Scheduler**. Per Microsoft, with Task Scheduler, we can create and manage common tasks that our computer will carry out automatically at the times we specify.

A task can run an application, a script, etc., and tasks can be configured to run at any point. A task can run at log in or at log off. Tasks can also be configured to run on a specific schedule, for example, every five mins.

To view the scheduled tasks that are present on the system, click `Task Scheduler Library`. This will display all the scheduled tasks of the system. You can click on any of them to view their details. The screenshot below shows a scheduled task named `SystemInfoDailyLog` configured to run `every day at 10:00 AM`. Here, you will see the program or command that will run when the task is triggered.
![](Attachments/Pasted%20image%2020260815231141.png)

It is also important to note that some scheduled tasks are not recurring and are made to run just once at a specific time.
**To create a basic task, click on `Create Basic Task` under **Actions** (right pane)**
![](Attachments/Pasted%20image%2020260815231433.png)







1. **Shared Folder** >>  is where you will see a complete list of shares and folders shared that others can connect to.
 ![](Attachments/Pasted%20image%2020260815233101.png)

View Shares: Click on the "Shares" section to see all shared folders. To stop sharing a folder, right-click it and select "Stop Sharing."

Create a New Share: Right-click on "Shares" and select "New Share" to choose a folder on your device and share it with other devices on the network.

Manage Permissions: Right-click on any shared folder, select "Properties," and then go to the "Share Permissions" tab to control access rights (Full Control, Change, Read).

Monitor Connections (Sessions): Click on "Sessions" to see who is currently connected to your device over the network; you can disconnect any user by right-clicking on them and selecting "Close Session."

Open Files: View the files currently being read or accessed by network users in real-time.
>[!note]
if you see like this Image in the below that's mean the folder is hidden >>


![](Attachments/Pasted%20image%2020260816002516.png)
 To see all shared folder writes  the below command .....
 ```
 net share
 ```

To reach into folders 
**1. Open the Run Dialog Box**

- Press `Win + R` on your keyboard.
    

**2. Access the Shared Folder directly using UNC Path**

- In the Run dialog box, enter the UNC path using either the hostname or the target IP address:
    
    - Using IP Address: `\\192.168.1.X`
        
    - Using Hostname: `\\TARGET-PC-NAME`
        
- _Note:_ To access a hidden share, append the share name along with `$` at the end (e.g., `\\192.168.1.X\C$` or `\\192.168.1.X\SecretFolder$`).
    

**3. Authenticate to the Target System**

- When prompted, enter the valid credentials (username and password) for the target machine and press **Enter**.
    

### Alternative Method: Mapping a Network Drive (Persistent Access)

1. Open **File Explorer** (`Win + E`) and navigate to **This PC**.
    
2. Click on **Map network drive** from the top ribbon menu (or right-click **This PC** and select **Map network drive...**).
    
3. Select an available drive letter (e.g., `Z:`).
    
4. In the **Folder** field, enter the network share path (e.g., `\\192.168.1.X\SharedFolder`).
    
5. Check the box for **Reconnect at sign-in** if persistent access across reboots is required, then click **Finish**.


___
___

 2. **Event Viewer**.
Event Viewer allows us to view events that have occurred on the computer. These records of events can be seen as an audit trail that can be used to understand the activity of the computer system. This information is often used to diagnose problems and investigate actions executed on the system.

![](Attachments/Pasted%20image%2020260815231512.png)

___
___
3. (Performance Monitor - Perfmon)
![](Attachments/Pasted%20image%2020260815233505.png)

TO reach into its ?
```
win + R  than  perfmon 
```

### Uses
1. (Real-Time Monitoring)
![](Attachments/Pasted%20image%2020260815233817.png)

![](Attachments/Pasted%20image%2020260815234032.png)

___
___
**Device Manager** 
allows us to view and configure the hardware, such as disabling any hardware attached to the computer. 

![](Attachments/Pasted%20image%2020260815234542.png)

___
___
What is the **System Information** (`msinfo32`) tool?

Per Microsoft, "_Windows includes a tool called Microsoft System Information (Msinfo32.exe).  This tool gathers information about your computer and displays a comprehensive view of your hardware, system components, and software environment, which you can use to diagnose computer issues._"
System Summary will display general technical specifications for the computer, such as processor brand and model.

The  information in **System Summary** is divided into three sections:

- **Hardware Resources**
- **Components**
- **Software Environment



### so important tool  >> (msinfo.exe)

![](Attachments/Pasted%20image%2020260816010119.png)


___
___
# Resource Monitor

What is **Resource Monitor** (`resmon`)?

Per Microsoft, "_Resource Monitor displays per-process and aggregate CPU, memory, disk, and network usage information, in addition to providing details about which processes are using individual file handles and modules. Advanced filtering allows users to isolate the data related to one or more processes (either applications or services), start, stop, pause, and resume services, and close unresponsive applications from the user interface. It also includes a process analysis feature that can help identify deadlocked processes and file locking conflicts so that the user can attempt to resolve the conflict instead of closing an application and potentially losing data._"

![](Attachments/Pasted%20image%2020260816013607.png)

___
___
###  Registry Editor
The **Windows Registry** (per Microsoft) is a central hierarchical database used to store information necessary to configure the system for one or more users, applications, and hardware devices.

The registry contains information that Windows continually references during operation, such as:

- Profiles for each user
- Applications installed on the computer and the types of documents that each can create
- Property sheet settings for folders and application icons
- What hardware exists on the system
- The ports that are being used.

____
____




C:\Users\<USER>\AppData\Roaming\Microsoft\Windows\PowerShell\PSReadline\ConsoleHost_history.txt

ذا الملف مرتبط بـ **PSReadLine** ويحتوي على الأوامر التي تم إدخالها في جلسات PowerShell التفاعلية.











the important path for all windows tools ?

C:\ProgramData\Microsoft\Windows\Start Menu\Programs\Administrative Tools