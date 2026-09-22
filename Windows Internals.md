

## Windows Internals — Lesson 1

### Windows Internals

Windows Internals is the study of the internal architecture, components, data structures, and mechanisms used by the Windows operating system to manage processes, threads, memory, I/O, security, networking, and hardware resources.

### Windows NT

Windows NT is the operating-system architecture and family on which modern versions of Microsoft Windows are based.

### User Mode

User Mode is the restricted execution environment in which most applications run. Applications operating in User Mode have limited access to system resources and must request privileged operations through operating-system interfaces.

### Kernel Mode

Kernel Mode is a highly privileged execution environment used by core operating-system components and device drivers. Code running in Kernel Mode has significantly greater access to system resources than User Mode applications.

### Kernel

The Windows Kernel is a core component of the operating system responsible for low-level functions such as thread scheduling, synchronization, interrupts, and processor-related operations.

### Windows Executive

The Windows Executive is a collection of operating-system components that provide major system-management services, including process management, memory management, I/O management, object management, security, and configuration management.

### Process

A process is an execution environment that provides resources and a virtual address space for a running program.

### Process ID (PID)

A Process ID is a unique numerical identifier assigned by Windows to a process so that the operating system and other tools can identify it.

### Thread

A thread is the basic unit of execution within a process and represents a sequence of instructions that can be scheduled for execution by the operating system.

### Virtual Address Space

A virtual address space is the range of virtual memory addresses available to a process. Each process normally has its own isolated virtual address space.

### Handle

A handle is a reference provided by Windows that allows a process to access and interact with an operating-system object or resource.

### Object

An object is a system-managed resource represented and controlled by Windows through its object-management mechanisms.

### Access Token

An access token is a security structure associated with a process or thread that contains security information such as the user identity, group memberships, privileges, and integrity level used for access-control decisions.

### Hardware Abstraction Layer (HAL)

The Hardware Abstraction Layer is a Windows component that provides an abstraction between the operating system and certain hardware-specific details.

### System Call
the door between the User Mode and Kernel Mode


___
___
## Windows Architecture lesson 2

┌───────────────────────────────────────────┐
│              APPLICATIONS                 │
│ Chrome | PowerShell | Word | Malware     │
└─────────────────────┬─────────────────────┘
                      │
                      ▼
┌───────────────────────────────────────────┐
│              USER MODE                    │
│                                           │
│ Win32 APIs                                │
│ DLLs                                      │
│ NTDLL.dll                                  │
└─────────────────────┬─────────────────────┘
                      │
                      │ System Call
                      ▼
═════════════════════════════════════════════
                 KERNEL MODE
═════════════════════════════════════════════
                      │
          ┌───────────┴───────────┐
          │                       │
          ▼                       ▼
┌──────────────────┐    ┌──────────────────┐
│ Windows Executive│    │ Windows Kernel   │
│                  │    │                  │
│ Process Manager  │    │ Scheduling       │
│ Memory Manager   │    │ Interrupts       │
│ I/O Manager      │    │ Synchronization  │
│ Object Manager   │    │                  │
│ Security         │    │                  │
└──────────────────┘    └────────┬─────────┘
                                 │
                                 ▼
                        ┌─────────────────┐
                        │ Device Drivers  │
                        └────────┬────────┘
                                 │
                                 ▼
                        ┌─────────────────┐
                        │    Hardware     │
                        │ CPU/RAM/Disk/NIC│
                        └─────────────────┘

**`ntdll.dll`** هو أهم مكتبة برمجية في الـ User Mode لنظام ويندوز، ويُطلق عليها **"بوابة العبور"** أو الطبقة الدنيا (Lowest-level User-mode Layer) التي تفصل بين البرامج العادية ونواة النظام (Kernel).
**تنفيذ نداءات النظام (Syscall Dispatcher):** هذه هي وظيفتها الكبرى. البرامج العادية لا تستطيع القفز للكيرنل مباشرة؛ لذا تمر عبر `ntdll.dll`.


## 1. Executive lesson (3)
The Executive contains managers responsible for the various system functions.
Process Manager >> Processes ,Threads Threads , Process creation ,Process termination
Thread Manager
Virtual Memory Manager
I/O Manager
Object Manager
Security Reference Monitor
Configuration Manager
Plug and Play Manager
Power Manager



## 2. Memory Manager
Virtual Memory
Physical Memory
Pages
Page Tables
Working Sets
Memory Mapping
Paging

## Review Questions & Answers

**1. Why can't User Mode applications directly access the Kernel?**  
Because Windows uses privilege levels and protection mechanisms to isolate User Mode from Kernel Mode.

**2. What is the difference between User Mode and Kernel Mode?**  
User Mode runs most applications with restricted privileges, while Kernel Mode runs highly privileged system components and drivers.

**3. What is the difference between a Windows API and a System Call?**  
A Windows API provides interfaces for applications, while a System Call provides a controlled way to request services from the Kernel.

**4. What is NTDLL.dll?**  
NTDLL.dll is a fundamental User Mode system library that provides Native API functions and interfaces to Windows system services.

**5. What is the difference between a Process and a Thread?**  
A Process is an execution environment and resource container, while a Thread is the basic unit of execution within a Process.

**6. Why are Processes, Memory, Handles, Threads, and APIs important for Process Injection?**  
Because Process Injection involves accessing another process, manipulating its memory, and potentially executing code through its threads using Windows APIs.



____
____
##  what is the Processes

Program = File/code on the disk
Process = An execution environment for this program.


## 1. What does a  process contain?
Process
│
├── Virtual Address Space
├── Threads
├── Handles
├── Access Token
├── Loaded DLLs
└── Process Information

## PID ?
every process get  one of the **Process ID**. 

## **Thread:**  ?
The basic unit of execution within a process.

## **Parent Process:**  ?
The process that created another process.



>[! note ]
The process provides the environment and resources.
The thread executes the instructions.

Process
   │
   ├── Memory
   ├── Handles
   ├── PEB
   ├── Security Token
   │
   └── Thread
          ↓
       Executes Code

>[! important ]
>- **الـ Process (العملية):** هي مجرد **حاوية خاملة (Inert Container)**. لا تنفذ أي كود بنفسها، بل تحجز الموارد فقط (العناوين في الذاكرة، جدول الـ Handles، بنية الـ PEB، والـ Security Token).
>- 
     **الـ Thread (خيط المعالجة):** هو **وحدة التنفيذ الفعلية (Unit of Execution)**. هو الكيان الوحيد الذي يملك سجلات المعالج (CPU Registers) والـ Stack ويتحرك داخل المعالج لتنفيذ سطر كود واحد تلو الآخر.

>[! important ]
>بمجرد تشغيل الملف، ينشئ ويندوز الـ **Main Thread** إجبارياً لتنفيذ الكود، ولا يحتاج المبرمج لفعل أي شيء.
>


## what is happen when  creation the process ?
.exe
 ↓
CreateProcess
 ↓
Windows creates Process
 ↓
Virtual Address Space
 ↓
Security Token
 ↓
Threads
 ↓
DLLs loaded
 ↓
Execution

## what is the EPROCESS ?
It is a kernel data structure that represents a process within the kernel.
Kernel Mode
   │
   └── EPROCESS
        ├── PID
        ├── Process information
        ├── Security information
        ├── Threads
        └── Memory information
## what is the PEB  = Process Environment Block?
its contain the important info  about  process  environment  

## what is the TEB =  Thread Environment Block ?
A user-mode structure containing information specific to a thread
Each thread within a process has its own structure:
EX :
Process
│
├── Thread 1 → TEB 1
├── Thread 2 → TEB 2
└── Thread 3 → TEB 3

like 
Thread ID
Thread Local Storage (TLS)
privet environment info 


                 PROCESS
                    │
        ┌───────────┼───────────┐
        │           │           │
    EPROCESS       PEB       Threads
    Kernel         User          │
                              ┌───┼───┐
                              │   │   │
                            TEB  TEB  TEB





## what is the TLS (Thread Local Storage) ?
هو أسلوب لتخصيص **بيانات خاصة ومنفصلة لكل مسار معالجة (Thread)**، رغم أن جميع هذه المسارات تنتمي لنفس البرنامج (Process) وتتشارك نفس مساحة الذاكرة.
___
___
## what is the Threads ?
The process is the container, and the thread is what executes the instructions.
EX:
Process: chrome.exe
│
├── Thread 1 ── executes code
├── Thread 2 ── executes code
├── Thread 3 ── executes code
└── Thread 4 ── executes code

## Why we need the Threads ?
Because the program may need to perform multiple tasks simultaneously.
Thread 1 → User Interface
Thread 2 → Network
Thread 3 → File operations
Thread 4 → Background work


## What does the thread possess?
Thread
├── Thread ID (TID)
├── CPU Registers
├── Stack
├── Execution Context
├── Scheduling information .>> It decides which thread gets the CPU now.
└── TEB

## what is the Context Switch ?
الـCPU لا يستطيع تنفيذ كل الـThreads في نفس اللحظة على نواة CPU واحدة.
Context Switch = الانتقال من Thread إلى Thread آخر مع حفظ واستعادة حالة التنفيذ

___
___
## KTHREAD & ETHREAD lesson (7)

- ***ETHREAD*:** A kernel data structure representing a Windows thread at the Executive level.  int locate in <mark style="background: #FFB86CA6;">Kernel Memory</mark>
- ***KTHREAD*:** A kernel data structure containing core information used to manage a thread's execution and scheduling. int locate in<mark style="background: #FFB86CA6;"> Kernel Memory</mark>
- **EPROCESS:** A kernel data structure representing a process.
- ***Kernel Thread*:** A thread managed by the Windows kernel for execution and scheduling.
Thread
 ↓
TEB   int locate in the User-mode 
 ├── Thread information
 ├── TLS
 └── Thread-specific data

ETHREAD
   ↓
Executive information about Thread
   ↓
KTHREAD
   ↓
Kernel scheduling/execution information
### Now, a practical example.
1. open the windeb
2. open any program
![](Attachments/Pasted%20image%2020260910160800.png)
3. from file open the launch excitable (Advanced) or Attach  to process
![](Attachments/Pasted%20image%2020260910160946.png)

4. in windows command write the "  !<mark style="background: #FF5582A6;">peb</mark>   " to see all info about the **Process Environment Block (PEB)**
![](Attachments/Pasted%20image%2020260910161834.png)

5. in windows command write the "  !<mark style="background: #FF5582A6;">teb</mark>  " to see all info about the  **Thread environment block**
![](Attachments/Pasted%20image%2020260910162047.png)
**After that write the (~) to see all the threads in the process
![](Attachments/Pasted%20image%2020260910162243.png)


## why all threads starts with the (6cdc)?
*because all threads belong to the same process* 

PROCESS
   │
   ├── PEB
   │
   └── THREADS
          │
          ├── TEB
          ├── TEB
          └── TEB

___
___
## CPU Scheduling & Thread Priority(Lesson 8)

The scheduler examines the ready threads and selects the one with the highest priority.

          CPU
           ↑
           │
       Scheduler
           ↑
   ┌───────┼────────┐
   │       │        │
Thread A Thread B Thread C
Priority  Priority  Priority
   8         13        6
## **Context Switch** ؟
It is the state the CPU needs to know:
Where was I? What was I doing? And how do I continue from the same point?


## Among the most important elements within the Context are:
CPU Registers
Instruction Pointer / RIP
Stack Pointer / RSP
Processor state information
Thread-related information

Processes
    ↓
Threads
    ↓
Thread Priority
    ↓
Scheduler
    ↓
Ready / Running / Waiting
    ↓
Scheduler chooses Thread
    ↓
Context Switch
    ↓
CPU Registers / Execution Context
    ↓
CPU executes selected Thread


___
___
## 9. Synchronization ؟

What happens when more than one thread attempts to access the same resource at the same time?

**Synchronization:**  
Mechanisms used to coordinate concurrent threads and safely access shared resources.

**Race Condition:**  
A condition where program behavior depends on the timing or ordering of concurrent operations.

**Critical Section:**  
A region of code that must be executed with controlled access to a shared resource.

**Mutex:**  
A synchronization object that provides exclusive ownership of a resource.

**Semaphore:**  
A synchronization object that allows a limited number of threads to access a resource concurrently.

**Event:**  
A synchronization object used to signal that a particular condition or event has occurred.

___
___
## Deadlock

### what is the Deadlock?
Deadlock is a situation where threads are waiting for each other, and none of them can proceed.
EX:
┌──────────────┐
│   Thread A   │
│ owns Lock 1  │
│ waits Lock 2 │
└──────┬───────┘
       │
       ▼
    Lock 2
       │
       ▲
       │
┌──────┴───────┐
│   Thread B   │
│ owns Lock 2  │
│ waits Lock 1 │
└──────────────┘

## If you really want to understand deadlock, don't just memorize the definition. ?
*Always ask four questions*
1. Which resource is being locked?
2. Who holds the lock?
3. Who is waiting for the lock?
4. Is there a circular wait?


___
---
## 10. Virtual Memory
الـ **Virtual Memory** هي آلية تجعل كل Process يرى مساحة عناوين افتراضية خاصة به.
Memory management system/mechanism
It may use RAM and disk.
Paging is used to manage this transfer.
EX:
Process A
Virtual Address Space
│
├── Code
├── DLLs
├── Heap
├── Stack
└── Data
## What happens when RAM becomes completely full ?
1. 1. Enabling virtual memory (Paging / Swapping)
2. The operating system moves inactive memory pages (data from programs open in the background that are not currently in use) from RAM to the hard drive (SSD or HDD).

			This data is stored in a dedicated file:
			In Windows: It is called pagefile.sys.


Virtual Memory          Physical RAM

Page 0 ───────────────→ Frame 7
Page 1 ───────────────→ Frame 21
Page 2 ───────────────→ Frame 3
Page 3 ───────────────→ Frame 50
Each page can have its own permissions
Page
├── Read
├── Write
└── Execute
## Page Tables ?
Page Table تخبر النظام: عندما يستخدم البرنامج هذا العنوان الافتراضي، أين توجد الصفحة المقابلة في الذاكرة الفيزيائية، وما صلاحياتها؟

خريطة يستخدمها Windows لتحويل عناوين الذاكرة الافتراضية إلى مواقع فعلية في الذاكرة.


Page Tables = الخريطة التي تخبر Windows أين توجد بيانات الـVirtual Memory فعليًا وكيف يمكن الوصول إليها.

> **Page Table لا تخزن البيانات نفسها؛ هي تساعد في تحديد أين توجد الصفحة فعليًا وكيف يمكن الوصول إليها.**
## Offset? 
```
       └── Which byte inside the Page?
```
>[!important ] 
>**Page = جزء من Virtual Memory**  
**Frame = المكان المقابل لها في Physical RAM**  
**Mapping = العلاقة بينهما.**



###  A program wants to access: Virtual Address
                    Virtual Address
                     │
          ┌──────────┴──────────┐
          │                     │
       Indices                Offset
          │                     │
          ▼                     │
        PML4                     │
          ↓                      │
        PDPT                     │
          ↓                      │
         PD                      │
          ↓                      │
         PT                      │
          ↓                      │
   Physical Frame                │
          │                      │
          └──────────┬───────────┘
                     ▼
              Physical Address
                     │
                     ▼
                    RAM

## CR3 ? 
يخبر المعالج أين يجد قاعدة/بداية بنية Page Tables الخاصة بمساحة العناوين الحالية


CR3
 ↓
PML4
 ↓
PDPT
 ↓
PD
 ↓
PT
 ↓
Physical Frame


## important EX >>
PROCESS
   │
   ▼
Virtual Address Space
   │
   ▼
Virtual Address
   │
   ▼
Page Tables
   │
   ├── PML4
   ├── PDPT
   ├── PD
   └── PT
   │
   ▼
Physical Frame
   │
   ▼
RAM




### 1. ما هي Virtual Page 5؟

هي **قطعة من الـVirtual Address Space** الخاصة بالـProcess.

إذا كان حجم الصفحة **4 KB**:

```
Virtual Address Space
┌──────────────┐
│ Page 0       │  4 KB
├──────────────┤
│ Page 1       │  4 KB
├──────────────┤
│ Page 2       │  4 KB
├──────────────┤
│ Page 3       │  4 KB
├──────────────┤
│ Page 4       │  4 KB
├──────────────┤
│ Page 5       │  4 KB  ← هذه
└──────────────┘
```

### 2. ما هو Physical Frame 20؟

هو **قطعة فعلية من RAM** حجمها أيضًا 4 KB.

```
Physical RAM
┌──────────────┐
│ Frame 0      │
├──────────────┤
│ Frame 1      │
├──────────────┤
│ ...          │
├──────────────┤
│ Frame 20     │  4 KB ← هذه
├──────────────┤
│ Frame 21     │
└──────────────┘
```



Page = الحافلة
Offset = رقم المقعد
Data = الشخص الجالس في المقعد
Offset يقول: أين بالضبط داخل هذه الصفحة؟
**Page → Frame** تحدد _أي منطقة في RAM_.

---
---

## Page Faults ؟
Page Fault يعني أن المعالج لا يستطيع إكمال الوصول إلى الذاكرة بالحالة الحالية، فيتدخل Windows لمعالجة الوضع. 




___
---
## Memory Manager ?
It is one of the core components of the Windows Executive, and its primary responsibility is memory management.

- Virtual Address Space
- Physical RAM
- Pages
- Page Tables
- Page Faults
- Working Sets
- Paging
- Memory Protection
                            **Windows Memory Manager.**

##  Working Set ?
كل Process لديه مجموعة من الصفحات الموجودة حاليًا في الذاكرة الفيزيائية والمستخدمة فعليًا من ذلك الـProcess.


## PEB and DLLs  ?
**One of the most important aspects of program analysis is knowing:**

What are the DLLs present within a process?
EX:
normal.exe
 ├── KERNEL32.dll
 ├── KERNELBASE.dll
 ├── USER32.dll
 └── suspicious.dll   ←  .>> its requires  investigation
 
# TEB ?
TEB
├── Thread ID
├── Stack information
├── TLS
├── Pointer to PEB
├── Thread environment
├── Last Error information
└── Other thread-specific data

## Why does every thread need its own TEB ?
because every thread has  its own status 
___
---
---




# Object Manager & Handles

## what is the Object Manager ?
its primary job is  manage the object  that OS  app initiate 
وظيفته الأساسية هي إدارة الـObjects التي ينشئها ويستخدمها النظام والبرامج


## Handle
الـHandle هو **مرجع يستخدمه Process للوصول إلى Object يديره Windows**.
	the app  not need to know the  physical location of object in kernel memory but it will use (Handle)

Process
   │
   │ Handle = 0x1234
   ↓
Windows Handle Table
   │
   ↓
Object


every process have  its own Handle Table
EX:
Process A
Handle Table
┌────────┬──────────────┐
│ Handle │ Object       │
├────────┼──────────────┤
│ 0x40   │ File Object  │
│ 0x44   │ Process Obj. │
│ 0x48   │ Event Object │
│ 0x4C   │ Token Object │
└────────┴──────────────┘
 >[!note ]
 >البرنامج لا يتعامل مباشرةً مع كثير من موارد Windows؛ بل يتعامل معها كـ Objects، ويصل إليها غالبًا عن طريق Handle.



## important Example 
1. Let's assume the program wants to open: C:\Test\secret.txt
2. 1. The program calls CreateFile. In User Mode, the program can use the Windows API: ''CreateFile(...)'' >>However, `CreateFile` does not mean that the program has directly entered kernel mode.
 Rather, the journey begins via Windows APIs, then proceeds through system calls to the kernel.
 Application
    ↓
Windows API
    ↓
NTDLL
    ↓
System Call
    ↓
Kernel
3. the Request enteres the Kernel >>The Windows kernel now receives the file open request.
 At this point, Windows begins checking several things, including:

Does the file exist?
Is the path correct?
Does the user have access rights?
What type of access is required?
Are there any security restrictions?

        USER MODE
┌─────────────────────────┐
│ Application             │
│                         │
│ CreateFile()            │
└────────────┬────────────┘
             ↓
        Windows API
             ↓
          NTDLL
             ↓
       System Call
             ↓
        KERNEL MODE
┌─────────────────────────┐
│ Security Check          │
│          ↓              │
│ Object Manager / I/O    │
│          ↓              │
+
│          ↑              │
│ Handle Table             │
└────────────┬────────────┘
             ↓
       Handle = 0x58
             ↓
        USER MODE
             ↓
       Application

##  Seeing Handles in Action 🔎
notepad++.exe

notepad++.exe
      │
      ↓
Handle Table
      │
 ┌────┼─────┐
 ↓    ↓     ↓
File Event  Mutex

### What does "Handle to File" mean?
 that mean another opened file
### What does "Handle to process" mean?
فهذا يعني أن A حصل على مرجع يسمح له بالتعامل مع Process B وفق **صلاحيات الوصول الموجودة على ذلك الـHandle**.



"ProcessExplorer" to see the handles
![](Attachments/Pasted%20image%2020260911205923.png)

![](Attachments/Pasted%20image%2020260911210440.png)

### What is the list of handles that a process uses to access objects?

Type       Name
File       C:\Users\HP\...
Key        HKLM\SOFTWARE\...
Event      \KernelObjects\...
Section    \Sessions\2\...

>[! note ]
>الـHandles تعطينا نافذة على الموارد التي يتعامل معها الـProcess.


![](Attachments/Pasted%20image%2020260911212357.png)



###  But there is a more important question: How do I know "what it ### does" with the object?

We need to add:      "Type +Name+Handle+Granted Access+Process+Activity"
EX:
Process A
    │
    └── Handle
          │
          ├── Type: Process
          ├── Target: Process B
          └── <mark style="background: #FF5582A6;">Access</mark>: ؟؟؟؟
          Access Rights = What you are allowed to do through that Handle
**Access is what tells us: What can Process A do with this handle?

## To view the permissions in detail, we often use WinDbg with the command:
![](Attachments/Pasted%20image%2020260911213945.png)






## These paths require attention.
%TEMP%
%APPDATA%
%LOCALAPPDATA%
%PUBLIC%
%USERPROFILE%\Downloads


































## what is the Mutant ?
### 1. التحكم في الوصول المتزامن (Mutual Exclusion)

الوظيفة البرمجية الأساسية لـ Mutant هي منع أكثر من مسار تنفيذ (Thread) أو عملية (Process) من الوصول إلى مورد مشترك (مثل ملف، مقطع من الذاكرة، أو منفذ اتصال) في الوقت نفسه
### 2. ضمان تشغيل نسخة واحدة فقط من البرنامج (Single Instance Execution)










Application
    ↓
CreateFile()
    ↓
Windows API
    ↓
System Call
    ↓
Kernel
    ↓
I/O Manager
    ↓
File System Driver
    ↓
Storage Driver
    ↓
Disk





Windows
   ↓
HAL
   ↓
Hardware



# Access Token

الـ Token يحمل معلومات أمنية عن السياق الذي يعمل به الـ Process، مثل:

```
User SID
Group SIDs
Privileges
Integrity Level
```

مثلاً:







![](Attachments/Pasted%20image%2020260911002940.png)