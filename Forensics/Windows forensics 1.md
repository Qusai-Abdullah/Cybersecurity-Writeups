Windows Forensics is the process of collecting, examining, and analyzing digital artifacts from a Windows system to determine user activities and events that occurred on the computer.


## Windows Registry:**  >>"regedit.exe,"
The Windows Registry is a collection of databases that contains the system's configuration data
**This configuration data can be about the hardware, the software, or the user's information. It also includes data about the recently used files, programs used, or devices connected to the system.

##  What is The a Registry Hives? >> 
C:\Windows\System32\Config\
> **are files that store portions of the Windows Registry, containing system, user, security, and application configuration data that can be analyzed as forensic artifacts.**
https://learn.microsoft.com/en-us/windows/win32/sysinfo/registry-hives#:~:text=Registry%20Hives.%20A%20hive%20is%20a%20logical%20group,with%20a%20separate%20file%20for%20the%20user%20profile.


## Structure of the Registry:
The registry on any Windows system contains the following five root keys:

1. HKEY_CURRENT_USER
2. HKEY_USERS
3. HKEY_LOCAL_MACHINE
4. HKEY_CLASSES_ROOT
5. HKEY_CURRENT_CONFIG

|Registry hive|Supporting files|
|---|---|
|HKEY_LOCAL_MACHINE\SAM|Sam, Sam.log, Sam.sav|
|HKEY_LOCAL_MACHINE\Security|Security, Security.log, Security.sav|
|HKEY_LOCAL_MACHINE\Software|Software, Software.log, Software.sav|
|HKEY_LOCAL_MACHINE\System|System, System.alt, System.log, System.sav|
|HKEY_CURRENT_CONFIG|System, System.alt, System.log, System.sav, Ntuser.dat, Ntuser.dat.log|
|HKEY_USERS\DEFAULT|Default, Default.log, Default.sav|


NTUSER.DAT .>> What is in the user's environment and settings? `C:\Users\<username>\`.
USRCLASS.DAT = What is contained in the Classes section and the Windows Shell environment for the user?   `C:\Users\<username>\AppData\Local\Microsoft\Windows`



### If you want to investigate a device and find out: Was a specific program running on the device? >> 
C:\Windows\AppCompat\Programs\Amcache.hve
Windows creates this hive to save information on programs that were recently run on the system

## What is the path for the five main registry hives, DEFAULT, SAM, SECURITY, SOFTWARE, and SYSTEM?
C:\Windows\System32\Config

## What is the path for the AmCache hive?


## **Transaction Logs and Backups:**
Transaction >> Data change log
Backups >> Backup of Hive 

