**Write access** control to any file on the system, regardless of the files ACL. You can **modify services**, DLL Hijacking, set **debugger** (Image File Execution Options)… A lot of options to escalate.

## DESCRIPTION

![[Pasted image 20230627163029.png]]

**!!NOTA IMPORTANTE!!** 

if ==SeRestorePrivilege== listed then

- Run [EnableSeRestorePrivilege.ps1](https://github.com/gtworek/PSBits/blob/master/Misc/EnableSeRestorePrivilege.ps1) to enable this privilege to our PowerShell session. We now have write access to ==C:\Windows\System32==.
- Aquí esta el binario: https://github.com/dxnboy/redteam/blob/master/SeRestoreAbuse.exe

#### Mas información
* https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Methodology%20and%20Resources/Windows%20-%20Privilege%20Escalation.md


## EXPLOITATION

1. Descargamos el binario: https://github.com/dxnboy/redteam/blob/master/SeRestoreAbuse.exe

2. Lo transferimos al a maquina:

```
#Por ejemplo usando WinRM
upload /home/kali/pg/heist/privescalation/SeRestoreAbuse.exe
```

3. Ejecutamos:

Cuidado con el comando que ejecutamos, mejor crear una shell o subir un nc antes:

```
./SeRestoreAbuse.exe "C:\\programdata\shell.exe"
```

![[Pasted image 20230627164438.png]]
## MACHINES

* Hack The Box: 
* PG: Heist