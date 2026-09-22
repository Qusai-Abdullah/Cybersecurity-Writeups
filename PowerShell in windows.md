
## 1. Fundamentals
1. what is the PowerShell .?
It is a shell and scripting language developed by Microsoft for managing operating systems, software, and resources, as well as executing commands and automating tasks. its handles with object 

```
Write-Host "Hello PowerShell"
```
its only display it on screen without save it 

2. 4. What is a Cmdlet ? 
It is a specialized PowerShell command that performs a specific task. Its name often consists of two parts: (Verb-Noun)
* Get >> what do you want to do 
* service >> What should I work on?

| Cmdlet          | الوظيفة             |
| --------------- | ------------------- |
| `Get-Process`   | عرض العمليات        |
| `Get-Service`   | عرض الخدمات         |
| `Get-Date`      | عرض التاريخ والوقت  |
| `Get-Location`  | معرفة المسار الحالي |
| `Get-ChildItem` | عرض محتويات مجلد    |
| `Get-Command`   | البحث عن الأوامر    |
| `Get-Help`      | الحصول على المساعدة |
$PSVersionTable >> display the version of Powershell


| the comannd                | what should doing                                     |
| -------------------------- | ----------------------------------------------------- |
| Get-Location               | dive you the current path                             |
| Get-ChildItem              | Displays the contents of the current path.            |
| Get-Command *service *     | search for all commands that containt  the "service " |
| get-help Get-Process -Full | all info and explaining how using it                  |
| Get-Command -Verb New      | search for verb                                       |
| Get-Command -noun service  | search for name                                       |
| Get-Help    Get-Process    | to know how can use it                                |
| Get-Process  explorer      |                                                       |

#### for  just understand all command without memorize it  save those five commands 
```
1. Get-Command *keyword*
2. Get-Help Command
3. Get-Help Command -Examples
4. Get-Help Command -Full
5. Command | Get-Member
```

___
---
### Objects & Pipeline  lesson (2)🔥

in PowerShell when you execute the  *Get-Process*  >>
The result is not just text; PowerShell receives objects representing the processes.


Get-Process | Select-Object Name, Id
Get-Process | Sort-Object Name
Get-Process | Select-Object -First 5
Get-Process | Select-Object -First 5


## Filter
```
get-process | where-object name -eq "chrome"
Get-Process | Where Name -eq "chrome"
```

| Operator | المعنى                      |
| -------- | --------------------------- |
| `-eq`    | Equal                       |
| `-ne`    | Not Equal                   |
| `-gt`    | Greater Than                |
| `-lt`    | Less Than                   |
| `-ge`    | Greater or Equal            |
| `-le`    | Less or Equal               |
| `-like`  | Pattern matching            |
| `-match` | Regular expression matching |
|          |                             |
|          |                             |
```
Get-Process | Where-Object CPU -gt 500
get-service | where-object status -eq runing
Get-Service | Where-Object Status -eq "stopped" | Select-Object name 
Get-Process | Where-Object name -eq "explorer" | Select-Object name , id
```


---
---

###  Variables, Data Types & Operators lesson (3)
#### what is the variable ?
It is a place where we store value for later use. its starts with <$>
```
$name ="qusai"

$name = "Sarah"
$age = 25
$isAdmin = $true
```
##  Comparison Operators
| Operator | المعنى                |
| -------- | --------------------- |
| `-eq`    | Equal                 |
| `-ne`    | Not Equal             |
| `-gt`    | Greater Than          |
| `-lt`    | Less Than             |
| `-ge`    | Greater Than or Equal |
| `-le`    | Less Than or Equal    |

---
---
##  Conditions & Control Flow lesson (4)
```
$age = 25

if ($age -ge 18) {
    Write-Host "Adult"
}
```

```
$age = 15

if ($age -ge 18) {
    Write-Host "Adult"
}
else {
    Write-Host "Minor"
}
```

```
$age = 20

if ($age -lt 13) {
    Write-Host "Child"
}
elseif ($age -lt 18) {
    Write-Host "Teenager"
}
else {
    Write-Host "Adult"
}
```


___
---
## Loops 🔄 lesson(5)
1. `foreach`


```
   $names = "Ali", "Ahmed", "Sarah"

foreach ($name in $names) {
    Write-Host $name
}


```

```
foreach ($name in $names ){Write-Host $name}
```

##  foreach with Objects 🔥

```
1. $processes = Get-Process
2. $processes
3. foreach ($process in $processes) {
    Write-Host $process.Name
}
```
## `foreach` with more than one of Property
```
foreach ($process in Get-Process) {
    Write-Host $process.Name $process.Id
}
```
##  `foreach` with Services
```
foreach ($service in Get-Service) {
    Write-Host $service.Name
}
```

>[! note ]
>use the pipline instead of foreach     |    
>

```
Get-Process | Select-Object Name, Id
```

Full Example :
```
foreach ($process in Get-Process) {
    if ($process.CPU -gt 100) {
        Write-Host $process.Name
    }
}


instead of  >>

Get-Process |
    Where-Object CPU -gt 100 |
    Select-Object Name
```
## break
```
foreach ($number in 1..10) {

    if ($number -eq 5) {
        break
    }

    Write-Host $number
}
```


## 1. Strings & Formatting في PowerShell lesson (6)

#### what the difference between the '' ''   and  '  ' ?
" "  >> it will replace the variable 
'   ' >> its not replace the variable only print all thing


#### `$()` — Subexpression
```
$process = Get-Process | Select-Object -First 1

"Name: $($process.Name)"
"PID: $($process.Id)"
```

" "          → Variable expansion
' '          → Literal string

$()          → Subexpression

```
.ToUpper()   → Uppercase
.ToLower()   → Lowercase
.Trim()      → Remove surrounding spaces
.Contains()  → Search
.Replace()   → Replace text
.Split()     → Split string

-split       → String → parts
-join        → parts → String

-like        → Wildcard matching
-match       → Regex matching
-replace     → Replace text

Select-Object → Select object properties
Format-Table  → Format display
Format-List   → Detailed display


```


___
___
## Function  Lesson (6)

```
function Get-SystemInfo {
    Get-Date
    Get-Process
    Get-Service
    than 
    Get-SystemInfo
}
```

PS C:\Users\HP> function hello{Write-Host "peace on you "}
PS C:\Users\HP> hello
peace on you
PS C:\Users\HP>


```
function Add-Numbers {
    param(
        [int]$A,
        [int]$B
    )

    $A + $B
}
```

```
function usage {Get-Process |Where-Object cpu -gt 100}     *usefull*
```



###  Function with Cybersecurity Job

```
function Check-User {
    param(
        [Parameter(Mandatory)]
        [string]$Username
    )

    Get-ADUser -Identity $Username -Properties Enabled,LastLogonDate
    
    
    than 
    Check-User -Username Sarah
}
```

## PROFILE  Lesson (7) <mark style="background: #FF5582A6;">>>>>>>>>>>>>>>>>>>></mark>
if you want save the function for all time you  can use  *$PROFILE*
![](Attachments/Pasted%20image%2020260922230141.png)

## what is the Profile ?
1. Any file where you put things that you want to have ready for you whenever you open PowerShell.

EX :
```
Aliases:
       Set-Alias ll Get-ChildItem
       Set-Alias grep Select-String
       
       Than 
        use ll
```
 2.  if you want make any function 
	```
	function myproject {
    Set-Location "C:\Users\Qusai\Projects"
    
    Than :
    use myproject
}
	```

2. for create this file if it not exist >> New-Item -Path $PROFILE -ItemType File -Force
   ``` 
   PS C:\Users\HP> Test-Path $PROFILE
True
PS C:\Users\HP>
   ```
![](Attachments/Pasted%20image%2020260922234602.png)
3. ![](Attachments/Pasted%20image%2020260922234643.png)
4.  Another EX :
    ![](Attachments/Pasted%20image%2020260922235837.png)
    ![](Attachments/Pasted%20image%2020260922235858.png)


##  A useful example for you as a cybersecurity student. <mark style="background: #FF5582A6;">>>>>>>>>>>>>>>>>></mark>
```
function lab {
    Set-Location "C:\CyberLab"
}

function procs {
    Get-Process |
        Sort-Object CPU -Descending |
        Select-Object -First 10 Name, Id, CPU
}

function ports {
    Get-NetTCPConnection |
        Where-Object State -eq "Listen" |
        Select-Object LocalAddress, LocalPort, OwningProcess
}

than you can use any one of command when you enter into Powershell 
1. ports
2. lab 
3. procs
```


___
___
___
## Error Handling Lesson (8)
####  1. Error 
$Error >> it save the session error
$Error[0] >> to display the last error 
$Error.Count >> to know number of errers
#### 2. ErrorAction 
```
Get-Item C:\NotExist.txt -ErrorAction SilentlyContinue
```
Execute the command, and if an error occurs, do not display it to the user.

```
try {
    Get-Item C:\NotExist.txt -ErrorAction Stop
}
catch {
    Write-Host "An error occurred"
}
```















Enable-PSRemoting -Force
Get-Service WinRM
New-Item -Path C:\CYNUserAccess -ItemType Directory -Force
### From the Windows client:
Set-Item WSMan:\localhost\Client\TrustedHosts -Value "192.168.10.10" -ForceExit-PSSession
Get-Item WSMan:\localhost\Client\TrustedHosts
Enter-PSSession -ComputerName 192.168.10.10 -Credential Administrator



## نبدأ JEA
الآن نريد تحويل الاتصال من:

> "Administrator يستطيع تنفيذ كل شيء"

إلى:

> "المستخدم qusai يستطيع تنفيذ أوامر محددة فقط."

1. Exit-PSSession





### الخطوة 2 — على Windows Server
1. New-Item -Path C:\CYNUserAccess -ItemType Directory -Force    انشاء مجلد ال jea
2. New-Item -Path C:\CYNUserAccess\RoleCapabilities -ItemType Directory -Force
3. New-PSRoleCapabilityFile -Path C:\CYNUserAccess\RoleCapabilities\qusaiRole.psrc
4. New-PSSessionConfigurationFile -Path C:\CYNUserAccess\CYNEndpoint.pssc -SessionType RestrictedRemoteServer
5. notepad C:\CYNUserAccess\CYNEndpoint.pssc


 لعمل عمليه الصح 
Test-PSSessionConfigurationFile -Path C:\CYNUserAccess\CYNEndpoint.pssc
![](Attachments/Pasted%20image%2020260912220454.png)

Enter-PSSession -ComputerName 192.168.10.10 -ConfigurationName CYNUserAccess -Credential CNDV2\sarah   ملف الاتصال من اليوندوز 10 
Get-Service



**`.psrc` = ماذا يستطيع أن يفعل؟**  
**`.pssc` = من يدخل وبأي صلاحيات؟**






____
___


لتاكيد اتصال ال vpn  
``` 
 Get-Service -Name "SEVPNSERVER"
```


لتاكيد  ال poowershell  in windows10  64
Enter-PSSession -ComputerName 192.168.10.10 -ConfigurationName CYNUserAccess -Credential CNDV2\sarah



## useful commands
1.  winget Search "file.exe"
2.  winget search
3. scoop update *  >> Update all installed software with a single command:
4. foreach($p in $process ){if ($p.cpu -gt 100){Write-Host $p.cpu , $p.id}}