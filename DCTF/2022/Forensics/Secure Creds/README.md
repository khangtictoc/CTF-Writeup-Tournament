# Secure Creds

**Point**: 100

With the connection to the victim's computer you managed to dump the lsass.exe process. Can you get the password from the dump file?

**Author**: Pixel#1111

File: [lsass.zip](lsass.zip)

## Basic Knowledge:

Check file dump:

```
┌──(virus㉿virus)-[~/Desktop]
└─$ file lsass.DMP 
lsass.DMP: Mini DuMP crash report, 16 streams, Sat Apr  9 02:47:27 2022, 0x421826 type
```

"Mini DuMP crash report" ? Base on this [source](http://crashrpt.sourceforge.net/docs/html/using_minidump.html#:~:text=A%20crash%20minidump%20file%20(DMP,%2C%20CPU%20count%2C%20etc.)%3B), a crash minidump file (DMP file) contains various information about the state of the application at the moment of time when it crashed. 

`lsass.exe` is a process thats verifies users logging on to a Windows computer or server, handles password changes, ... it handles sensitive data like hash password, logon name, LSA secret keys, ...

## Solution:

I've searched for _"extract password from lsass dump"_ and [this site](https://en.hackndo.com/remote-lsass-dump-passwords/) has suggested many tools to retrieve password from **lsass's dump file**. Most of result suggest use [Mimikatz](https://github.com/ParrotSec/mimikatz/tree/master). So i will use it to get password :

> NOTE: Make sure to turn off anti-virus. **Mimikatz** is detected as a malware

Use MiniDump to analyze: 

```
sekurlsa::minidump {path_to_dump_file}
```

![image](https://user-images.githubusercontent.com/48288606/163699215-3aa9d922-1436-4096-9533-aa05b977cfe8.png)

Get password for each user in each process:

```
sekurlsa::logonpasswords
```

![image](https://user-images.githubusercontent.com/48288606/163699276-a954ba47-2918-422e-b9e3-ddcae3a2057e.png)

Flag: **dctf{n0_ant1v1ru5_l0l}**
