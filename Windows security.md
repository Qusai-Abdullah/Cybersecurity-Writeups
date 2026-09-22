to make full screen in vm    
1. install vm tools
2. than enter to hards in  windows than run the added DVD






Q: What is the difference between SRM and LSASS in terms of operating mode and function?
1. SRM = security reference monitor  >>Enforcing security policies and access control & Is the user/process allowed to access a resource?
2.   LSASS = `Local Security Authority Subsystem Service|>> Who manages the authentication process and security policies?



SAM >> **Security Account Manager**، >> Storing local user account information.
C:\Windows\System32\config\SAM
___
- **BitLocker To Go:** ميزة مخصصة لتشفير وسائط التخزين القابلة للإزالة مثل أقراص USB الخارجية.
AppLocker & Software Restriction Policies (SRP)
Applocker is modern 
SRP is old 

secpol.msc
![](Attachments/Pasted%20image%2020260820232228.png)

we need to ensure the service is on or down ?
```    ctrol + R
services.msc
and search for thr (Application Identity)
```



ControlSet001 .>> **CurrentControlSet** هو الـ Control Set الذي يستخدمه Windows **حاليًا أثناء تشغيل الجهاز**:  
`HKLM\SYSTEM\CurrentControlSet`



**1. System Information & OS Version**

- **Registry Key:** `SOFTWARE\Microsoft\Windows NT\CurrentVersion`
    
- **Forensic Value:** Identifies OS product name (`ProductName`), exact build number (`CurrentBuildNumber`), and installation date (`InstallDate`).
    

**2. Control Sets & Current Configuration**

- **Registry Keys:** `SYSTEM\ControlSet001` and `SYSTEM\ControlSet002`
    
- **Selection Keys:**
    
    - `SYSTEM\Select\Current`: Points to the ControlSet used during the current boot.
        
    - `SYSTEM\Select\LastKnownGood`: Points to the last known stable configuration.
        
- **Forensic Value:** Verifies volatile configurations (`CurrentControlSet`) and detects persistence or driver modifications across reboots.
    

**3. Machine Identification & Time Zone**

- **Computer Name:** `SYSTEM\CurrentControlSet\Control\ComputerName\ComputerName`
    
- **Time Zone:** `SYSTEM\CurrentControlSet\Control\TimeZoneInformation`
    
- **Forensic Value:** Confirms target machine identity and establishes chronological event timelines by mapping local time to UTC.
    

**4. Network Activity & Past Connections**

- **Interfaces Configuration:** `SYSTEM\CurrentControlSet\Services\Tcpip\Parameters\Interfaces` (contains unique GUIDs with assigned IP, DHCP, and DNS settings).
    
- **Network History:**
    
    - `SOFTWARE\Microsoft\Windows NT\CurrentVersion\NetworkList\Signatures\Unmanaged`
        
    - `SOFTWARE\Microsoft\Windows NT\CurrentVersion\NetworkList\Signatures\Managed`
    - - **المسار:** `HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\NetworkList\Profiles`  
        
- **Forensic Value:** Tracks IP assignments, past network profiles, and connection timestamps via key last write times.
    

**5. Autostart Mechanisms (Persistence)**

- **User & System Run Keys:**
    
    - `NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\Run`
        
    - `SOFTWARE\Microsoft\Windows\CurrentVersion\Run`
        
- **Services Auto-Start:** `SYSTEM\CurrentControlSet\Services` (a `Start` value set to `0x02` indicates boot-time execution).
    
- **Forensic Value:** Uncovers malware persistence mechanisms designed to execute automatically upon system boot or user logon.
    

**6. User Accounts & Login Artifacts**

- **Registry Key:** `SAM\Domains\Account\Users`
    
- **Forensic Value:** Discovers user RIDs, logon counts, last login timestamp, last failed login attempt, password age/expiration, and group memberships.


### 1. استمرارية التشغيل للمستخدم (User-Level Persistence)

- **المسار:** `Software\Microsoft\Windows\CurrentVersion\Run` و `RunOnce`
    
- **الفائدة الجنائية:** يفحصه المحقق لاكتشاف البرمجيات الخبيثة التي تُقلع تلقائياً بمجرد دخول هذا المستخدم تحديداً دون الحاجة لصلاحيات مدير (Admin).
    

### 2. تتبع تشغيل البرامج وفك التشفير (UserAssist)

- **المسار:** `Software\Microsoft\Windows\CurrentVersion\Explorer\UserAssist`
    
- **الفائدة الجنائية:**
    
    - يسجل كل برنامج تم تشغيله عبر الواجهة الرسومية (GUI).
        
    - المفاتيح مشفرة بخوارزمية بسيطة اسمها **`ROT13`** (مثال: `pnyp.rkr` تعني `calc.exe`).
        - يمنحك: عدد مرات التشغيل (**Run Count**)، وتاريخ ووقت آخر تشغيل بدقة.
        - ![](Attachments/Pasted%20image%2020260823233021.png)





- **Amcache (`Amcache.hve`):** يسجل تفاصيل البرامج وتواريخ تثبيتها وتشغيلها وتجزئتها (Hashes).


### تصفح الملفات والمستندات (Recent Documents)

- **المسار:** `Software\Microsoft\Windows\CurrentVersion\Explorer\RecentDocs`
    
- **الفائدة الجنائية:**
    
    - يثبت وصول المستخدم لملفات معينة (سواء صور، ملفات PDF، سكريبتات).
        
    - مقسم حسب امتداد الملفات (مثلاً مجلد فرعي لـ `.docx` وآخر لـ `.ps1` وهكذا).
        
    - يعطيك الترتيب الزمني لفتح الملفات عبر قيمة `MRUListEx` (Most Recently Used).

### 4. البحث والأوامر المكتوبة (RunMRU & TypedPaths)

- **المسارات:**
    
    - `Software\Microsoft\Windows\CurrentVersion\Explorer\RunMRU`: كل أمر تم كتابته في نافذة تشغيل **Run** (مثل `cmd`, `powershell`, أو تشغيل برامج ضارة).
        
    - `Software\Microsoft\Windows\CurrentVersion\Explorer\TypedPaths`: المسارات والمجلدات التي كتبها المستخدم يدوياً في شريط مسار مستكشف الملفات (File Explorer).    فقط يسجل التي كتبتها في نافذة ال cmd 




### . أدلة التفاعل مع المجلدات وحفظ الملفات (ShellBags & OpenSave)

- **OpenSavePidlMRU:**
    
    - المسار: `Software\Microsoft\Windows\CurrentVersion\Explorer\ComDlg32\OpenSavePidlMRU`
        
    - يسجل كل ملف تم فتحه أو حفظه عبر النوافذ الحوارية داخل التطبيقات (Open/Save dialog).



![](Attachments/Pasted%20image%2020260823235023.png)
        
- **ShellBags:**
    
    - المسار: `Software\Microsoft\Windows\Shell\Bags` (وكذلك في `UsrClass.dat`).
        
    - يثبت دخول وتصفح مجلدات معينة على الجهاز أو الشبكة أو الفلاش ميموري حتى لو تم حذف المجلد لاحقاً.
    - **إثبات الوصول والتصفح:** تُثبت أن المستخدم قام بفتح وتصفح مجلد معين، حتى لو لم يتم تعديل 
    - أي ملف داخله.
    - **تتبع وحدات التخزين الخارجية والشبكية:** تسجل المجلدات التي تم تصفحها داخل فلاشات USB، أقراص خارجية، أو مجلدات مشاركة عبر الشبكة (Network Shares).










>[!note reg save HKCU D:\NTUSER.DAT /y]





___
___
## **Recent Files:**
Windows maintains a list of recently opened files for each user. As we might have seen when using Windows Explorer, it shows us a list of recently used files.  This information is stored in the NTUSER hive and can be found on the following location:

`NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\Explorer\RecentDocs`



![](Attachments/Pasted%20image%2020260823235534.png)

**أين تجد بيانات التصفح الفعلية والكاملة (ShellBags)؟** توجد الأدلة التفصيلية للمجلدات التي فتحها المستخدم داخل ملف **`UsrClass.dat`** لهذا المستخدم عبر المسار: `Local Settings\Software\Microsoft\Windows\Shell\BagMRU`

للوصول إليها، افتح ملف `UsrClass.dat` الخاص بالمستخدم (الموجود في مسار `AppData\Local\Microsoft\Windows\UsrClass.dat`
C:\Users\<Username>\AppData\Local\Microsoft\Windows\UsrClass.dat


## **Open/Save and LastVisited Dialog MRUs:**
When we open or save a file, a dialog box appears asking us where to save or open that file from. It might be noticed that once we open/save a file at a specific location, Windows remembers that location. This implies that we can find out recently used files if we get our hands on this information. We can do so by examining the following registry keys

`NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\Explorer\ComDlg32\OpenSavePIDlMRU`

![](Attachments/Pasted%20image%2020260824000815.png)


## **Windows Explorer Address/Search Bars:**
Another way to identify a user's recent activity is by looking at the paths typed in the Windows Explorer address bar or searches performed using the following registry keys, respectively.

`NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\Explorer\TypedPaths`

`NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\Explorer\WordWheelQuery`

### 

## Evidence of Execution


![](Attachments/Pasted%20image%2020260824001157.png)


**ShimCache**  or AppCompatCache ?
يحتوي على آثار عن **الملفات التنفيذية (Executables)** التي تعرّف عليها Windows أثناء تشغيل/فحص النظام.
### 🧪 أهميته في Digital Forensics

يستفيد منه المحقق الجنائي الرقمي لمعرفة أن ملفًا تنفيذيًا **كان موجودًا على النظام أو تم التعامل معه من قِبل Windows**.

SYSTEM/ControlSet00x\Control\Session Manager\AppCompatCache


ShimCache    توجد في اللوكل ماشين


| Artifact       | وظيفته الأساسية                                                                      | ماذا أستفيد منه؟                                           | مكانه                                                                                   |
| -------------- | ------------------------------------------------------------------------------------ | ---------------------------------------------------------- | --------------------------------------------------------------------------------------- |
| **UserAssist** | يتتبع برامج شُغّلت من خلال **Windows Explorer/واجهة المستخدم**                       | اسم البرنامج، وقت آخر تشغيل، وعدد مرات التشغيل             | `NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\Explorer\UserAssist\{GUID}\Count` |
| **ShimCache**  | آلية **Application Compatibility** في Windows                                        | معلومات عن الملفات التنفيذية مثل الاسم والحجم ووقت التعديل | `SYSTEM\CurrentControlSet\Control\Session Manager\AppCompatCache`                       |
| **AmCache**    | يخزن معلومات إضافية عن التطبيقات والملفات  غير محمّل بشكل دائم داخل واجهة `regedit`. | المسار، أوقات مختلفة، وSHA-1 في بعض الإدخالات              | `C:\Windows\AppCompat\Programs\Amcache.hve`                                             |
| **BAM**        | يتتبع نشاط التطبيقات في الخلفية                                                      | المسار الكامل وآخر وقت تشغيل/نشاط في بعض الأنظمة           | `SYSTEM\CurrentControlSet\Services\bam\UserSettings\{SID}   in local_mashice `          |
| **DAM**        | مرتبط بإدارة/تحسين نشاط التطبيقات والطاقة                                            | بيانات نشاط التطبيقات المرتبطة بـ Modern Standby           | `SYSTEM\CurrentControlSet\Services\dam\UserSettings\{SID}`                              |



![](Attachments/Pasted%20image%2020260824224315.png)




Amcache.hve أين تجد الهاش ؟

- في القائمة الشجرية على اليسار، اصعد إلى مجلد **`Root`**.
    
- ابحث عن المفتاح الجنائي الخاص بالملفات التنفيذية:
    
    - في أنظمة ويندوز 10 و 11 الحديثة: ادخل إلى **`InventoryApplicationFile`**.

What is another name for ShimCache?

AppCompatCache

Which of the artifacts also saves SHA1 hashes of the executed programs?

AmCache

Which of the artifacts saves the full path of the executed programs?

BAM/DAM






___
___
### External Devices/USB device forensics



in the local_machine + system 
When performing forensics on a machine, often the need arises to identify if any USB or removable drives were attached to the machine. If so, any information related to those devices is important for a forensic investigator. In this task, we will go through the different ways to find information on connected devices and the drives on a system using the registry.

#### Device identification:
The following locations keep track of USB keys plugged into a system. These locations store the vendor id, product id, and version of the USB device plugged in and can be used to identify unique devices. These locations also store the time the devices were plugged into the system.
```
SYSTEM\CurrentControlSet\Enum\USBSTOR
SYSTEM\CurrentControlSet\Enum\USB
```
These keys can contain information such as:

- **Vendor** – Device manufacturer.
- **Product** – Device model/product.
- **Version** – Device revision/version.
- **Serial Number** – Helps identify a unique physical device.

2. USB Connection Times 
|`0064`|First Connection Time|
|`0066`|Last Connection Time|
|`0067`|Last Removal Time|

 USB Volume Name
. The following Registry location can provide information about the device/volume name:
. SOFTWARE\Microsoft\Windows Portable Devices\Devices



























**. قواعد بيانات المتصفحات (Browser History Databases)** المتصفحات الحديثة (Chrome, Edge, Firefox, Brave) تخزن سجل التصفح الكامل، كلمات البحث، والتنزيلات داخل قواعد بيانات بصيغة **SQLite** في مجلدات الـ AppData للمستخدم:

- **Edge / Chrome:** `C:\Users\<User>\AppData\Local\Microsoft\Edge\User Data\Default\History`
    
    `C:\Users\<User>\AppData\Local\Google\Chrome\User Data\Default\History`
    
- **Firefox:** `C:\Users\<User>\AppData\Roaming\Mozilla\Firefox\Profiles\<Profile>\places.sqlite`


**. قاعدة بيانات سجل الأنشطة (Windows Activity History / Timeline)** يسجل ويندوز التطبيقات المفتوحة، الملفات المستعرضة، والبحث الداخلي مع تواريخ استخدامها في ملف SQLite مخصص:

- **المسار:**
    
    `C:\Users\<User>\AppData\Local\ConnectedDevicesPlatform\<ProfileGUID>\ActivitiesCache.db`



**ملفات الـ Prefetch و Shimcache و Amcache**

- **Prefetch (`C:\Windows\Prefetch`):** يثبت تشغيل أدوات ومحركات التصفح وأوقات تنفيذها وعدد مرات التشغيل.
    
- **Amcache / Shimcache:** يثبت وجود البرامج والمسارات حتى لو حُذفت الملفات أو لم يسجلها الرجستري في قوائم الـ Typed.


| **نوع الـ Hive / المفتاح الجذري**                        | **نطاق البيانات (Scope)**                             | **طبيعة المعلومات المخزنة فيه**                                                  | **أمثلة جنائية وتقنية شائعة**                                                                                                                                                                                                                                                      |
| -------------------------------------------------------- | ----------------------------------------------------- | -------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **`HKCU` / `NTUSER.DAT` & `UsrClass.dat`** _(User Hive)_ | **خاص بالمستخدم الحالي فقط** (Per-User)               | كل ما يفعله المستخدم من واجهته وتطبيقاته وتفضيلاته الشخصية.                      | • البرامج التي شغلها المستخدم (`UserAssist`)<br><br>  <br><br>• الملفات المفتوحة مؤخراً (`RecentDocs`)<br><br>  <br><br>• تصفح المجلدات (`Shellbags`)<br><br>  <br><br>• عمليات البحث في النظام (`WordWheelQuery`)<br><br>  <br><br>• بدء التشغيل التلقائي الخاص بالمستخدم (`Run`) |
| **`HKLM\SOFTWARE`** _(System-Wide Software)_             | **عام لكل مستخدمي الجهاز** (Machine-Wide)             | إعدادات البرامج المثبتة على مستوى النظام، تفاصيل إصدار الويندوز، وقوائم الشبكات. | • البرامج المثبتة على الجهاز (`Uninstall`)<br><br>  <br><br>• شبكات الاتصال السابقة (`NetworkList\Profiles`)<br><br>  <br><br>• برامج بدء التشغيل العامة لجميع الحسابات (`Run`)<br><br>  <br><br>• تفاصيل إصدار النظام (`CurrentVersion`)                                          |
| **`HKLM\SYSTEM`** _(System Hive)_                        | **العتاد، التعريفات، والنواة** (OS Kernel & Hardware) | إعدادات الإقلاع، برامج التشغيل (Drivers)، الخدمات (Services)، والشبكة المادية.   | • الفلاشات والأجهزة الخارجية المتصلة (`USBSTOR`)<br><br>  <br><br>• إعدادات كروت الشبكة والـ IP (`Tcpip\Parameters\Interfaces`)<br><br>  <br><br>• أسماء الخدمات المشغلة في الخلفية (`Services`)<br><br>  <br><br>• إعدادات إقلاع النظام (`ControlSet001`)                         |
| **`HKLM` عموماً** _(HKEY_LOCAL_MACHINE)_                 | **الجهاز ككل**                                        | هو "المظلة الكبرى" التي تضم `SAM`, `SECURITY`, `SOFTWARE`, `SYSTEM`.             | إعدادات الأمان العامة، حسابات المستخدمين المحلية (`SAM`)، وتكوينات العتاد والنظام بالكامل.                                                                                                                                                                                         |


The table below lists some registry keys that are particularly useful during forensic investigations.

| Registry Key                                                             | Importance                                                                                                           |
| ------------------------------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------- |
| `HKCU\Software\Microsoft\Windows\CurrentVersion\Explorer\UserAssist`     | It stores information on recently accessed applications launched via the GUI.                                        |
| `HKCU\Software\Microsoft\Windows\CurrentVersion\Explorer\TypedPaths`     | It stores all the paths and locations typed by the user inside the Explorer address bar.                             |
| `HKLM\Software\Microsoft\Windows\CurrentVersion\App Paths`               | It stores the path of the applications.                                                                              |
| `HKCU\Software\Microsoft\Windows\CurrentVersion\Explorer\WordWheelQuery` | It stores all the search terms typed by the user in the Explorer search bar.                                         |
| `HKLM\Software\Microsoft\Windows\CurrentVersion\Run`                     | It stores information on the programs that are set to automatically start (startup programs) when the users logs in. |
| `HKCU\Software\Microsoft\Windows\CurrentVersion\Explorer\RecentDocs`     | It stores information on the files that the user has recently accessed.                                              |
| `HKLM\SYSTEM\CurrentControlSet\Control\ComputerName\ComputerName`        | It stores the computer's name (hostname).                                                                            |
| `HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall`               | It stores information on the installed programs.                                                                     |


Hive: Software. Key: This key stores information on the installed programs ![](Attachments/Pasted%20image%2020260904001409.png)





___
___
Forensics (Senario)- Registry Furensics 
                         Story

TBFC is under attack. Systems are exhibiting weird behavior, and the company is now feeling the absence of its lead defender, McSkidy. However, McSkidy made sure the legacy continues.

McSkidy’s team, determined and well-trained, is fully confident in securing all the systems and regaining control before the big event, SOCMAS.

They have now decided to conduct a detailed forensic analysis on one of the most critical systems of TBFC, `dispatch-srv01`. The `dispatch-srv01` coordinates the drone-based gifts delivery during SOCMAS. However, recently it was compromised by King Malhare’s bandits of bunnies.

TBFC’s defenders have decided to split into specialized teams to uncover the attack on this system through detailed forensics. While some of the other team members investigate logs, memory dumps, file systems, and other artefacts, you will work to investigate the registry of this compromised system.

 1. طيب لمعرفة البربامج  الت تم تنزيلها بوقت محدد
 2. SOFTWARE/- `Microsoft\Windows\CurrentVersion\Uninstall`
 OR 
 HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall 

3. What application was installed on the `dispatch-srv01` before the abnormal activity started? 
    DroneManager Updater from software
4. ### ثانياً: إيجاد المسار الكامل الذي تم تشغيل البرنامج منه (Full Path)؟
 ### كيف تصل إلى هذا المسار بنفسك داخل Registry Explorer؟

يمكنك العثور على المسار الكامل عبر أحد الدليلين التاليين داخل ملف **`NTUSER.DAT`**:

1. **عبر مفتاح الـ UserAssist (المسار الأوضح للتنفيذ):**
    
    - اذهب إلى: `ROOT\Software\Microsoft\Windows\CurrentVersion\Explorer\UserAssist\{GUID}\Count`


___
____

طريقة حذف السجلات من قبلالمخترق 
**1. مسح وتضليل سجلات الأحداث (Windows Event Logs)**

- **المسح الشامل عبر الأدوات المدمجة (Log Clearing):**
    
    - استخدام أداة `wevtutil`:
        
    
        
        ```
        wevtutil cl Security
        wevtutil cl System
        wevtutil cl "Windows PowerShell"
        ```
        
    - أو عبر PowerShell:

    
    PowerShell
    
    ```
    Clear-EventLog -LogName Application, System, Security
    ```
    

_(هذا الفعل يولد فوراً الحدث الشهير `Event ID 1102` في سجل Security أو `Event ID 104` في_

**إيقاف خدمة السجلات في الذاكرة (Service Blinding / Thread Suspension):**

- بدلاً من مسح السجل وإثارة الانتباه، يتم تجميد أو إيقاف الـ Threads المسؤولة عن تسجيل الأحداث داخل عملية `svchost.exe` (EventLog Service) عبر أدوات مثل Mimikatz (`event::drop`) أو Phant0m، مما يجعل النظام يتوقف عن كتابة أي سجلات جديدة دون إيقاف الخدمة رسمياً.

**2. حذف وتعديل مفاتيح الـ Registry (Registry Tampering & Anti-Forensics)**

- **حذف مفاتيح التتبع والأدلة الجنائية:**
    
    - حذف مفاتيح تشغيل البرامج وقوائم الملفات المفتوحة عبر سطر الأوامر:
        
        DOS
        
        ```
        reg delete "HKCU\Software\Microsoft\Windows\CurrentVersion\Explorer\RunMRU" /va /f
        reg delete "HKCU\Software\Microsoft\Windows\CurrentVersion\Explorer\RecentDo
        ```



**كيف يكتشف المحقق الجنائي هذا التضليل؟**

- **فجوات التوقيت (Time Gaps):** انقطاع مفاجئ في توالي الأحداث دون إيقاف تشغيل الجهاز.
    
- **فحص الـ USN Journal و $MFT:** تظل أسماء الملفات المحذوفة وعمليات الحذف مسجلة في سجل معاملات نظام الملفات NTFS.
    
- **الـ Unallocated Space و Transaction Logs:** استخراج المفاتيح المحذوفة من ملفات الـ `.LOG` الخاصة بالـ Registry (Registry Transaction Logs).


`vssadmin` = 
أداة Windows للتعامل مع Volume Shadow Copies، وأهم استخدام بسيط لها في الـ Forensics هو معرفة الـ Shadow Copies الموجودة على الجهاز





**`$MFT` (Master File Table):** يحتوي على تفاصيل وسجلات الملفات التي تم حذفها، الطوابع الزمنية ($STANDARD_INFORMATION و $FILE_NAME)، مما يثبت توقيت الحذف والأداة المستخدمة.





### 3. أهم المفاتيح الموجودة داخلها (Structure):

عند فتحها، ستجد بداخلها مفاتيح فرعية هامة لأدلة التشغيل مثل:

- **`Root\InventoryApplicationFile`**: يحتوي على المسار الكامل للبرامج التنفيذية، الحجم، وتوقيع الـ **SHA-1 Hash** للملف.
    
- **`Root\InventoryApplication`**: يحتوي على تفاصيل البرامج المثبتة وتواريخ التثبيت.
    
- **`Root\InventoryDriverBinary`**: لمعلومات ملفات تعريف الأجهزة (Drivers).
    

> **ملاحظة جنائية:** الأسلوب الأسهل والأكثر دقة لتحليلها خارج `regedit` هو استخدام أدوات التحقيق المخصصة مثل **`AmcacheParser`** (من Eric Zimmerman) أو فتحها عبر **`Registry Explorer`**





___
___
___



**The Challenge:**

﻿Now that we know where the required toolset is, we can start our investigation. We will have to use our knowledge to identify where the different files for the relevant registry hives are located and load them into the tools of our choice. Let's answer the questions below using our knowledge of registry forensics.

**Scenario:**

One of the Desktops in the research lab at Organization X is suspected to have been accessed by someone unauthorized. Although they generally have only one user account per Desktop, there were multiple user accounts observed on this system. It is also suspected that the system was connected to some network drive, and a USB device was connected to the system. The triage data from the system was collected and placed on the attached VM. Can you help Organization X with finding answers to the below questions?

**Note:** When loading registry hives in RegistryExplorer, it will caution us that the hives are dirty. This is nothing to be afraid of. We just need to remember the little lesson about transaction logs and point RegistryExplorer to the .LOG1 and .LOG2 files with the same filename as the registry hive. It will automatically integrate the transaction logs and create a 'clean' hive. Once we tell RegistryExplorer where to save the clean hive, we can use that for our analysis and we won't need to load the dirty hives anymore. RegistryExplorer will guide you through this process.

What is the username of the account that has never been logged in?


![](Attachments/Pasted%20image%2020260828004851.png)

When was the file 'Changelog.txt' accessed?
2021-11-24 18:18:48        from    (UTUSER )


What is the complete path from where the python 3.8.2 installer was run?
**UserAssist يثبت التنفيذ الفعلي من قِبل المستخدم عبر الواجهة (GUI Execution):**
Z:\setups\python-3.8.2.exe
![](Attachments/Pasted%20image%2020260828030837.png)


When was the USB device with the friendly name 'USB' last connected?

the name of usb you will find it in  software      and the last connacted in system 
![](Attachments/Pasted%20image%2020260828032608.png)




___
____
shutdown /s /t 60