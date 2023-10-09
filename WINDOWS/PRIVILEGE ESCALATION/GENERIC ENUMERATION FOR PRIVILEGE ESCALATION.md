## ENUMERATION


https://book.hacktricks.xyz/windows-hardening/windows-local-privilege-escalation#alwaysinstallelevated



1. Comandos básicos:

```
whoami

whoami /groups

# En powershell

Get-LocalUser

Get-LocalGroup

Get-LocalGroupMember adminteam

#En cmd

systeminfo

ipconfig /all

route print

# To list all active network connections we can use netstat11 with the argument -a to display all active TCP connections as well as TCP and UDP ports, -n to disable name resolution, and -o to show the process ID for each connection.

netstat -ano

# Comprobar apps intaladas Powershell

Get-ItemProperty "HKLM:\SOFTWARE\Wow6432Node\Microsoft\Windows\CurrentVersion\Uninstall\*" | select displayname 
Get-ItemProperty "HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall\*" | select displayname


# Comprobar aplicaciones corriendo Powershell

Get-Process
```

2. Mirar permisos -> SeImpersonate privileges

3. Mirar permisos en directorio web: C:\xampp\htdocs\assets

4. Busqueda de ficheros interesantes:

```
Get-ChildItem -Path C:\xampp -Include *.txt,*.ini -File -Recurse -ErrorAction SilentlyContinue

#Enumerar en un usuario

Get-ChildItem -Path C:\Users\dave\ -Include *.txt,*.pdf,*.xls,*.xlsx,*.doc,*.docx -File -Recurse -ErrorAction SilentlyContinue
Get-ChildItem -Path C:\Users\dave\ -Include *.txt,*.pdf,*.xls,*.xlsx,*.doc,*.docx -File -Recurse -ErrorAction SilentlyContinue
```

INTERESANTE: `type C:\xampp\mysql\bin\my.ini`

3. Ver el historial:

```
Get-History

(Get-PSReadlineOption).HistorySavePath

```

![[Pasted image 20230611154656.png]]
4. Buscar transcript, por ejemplo en C:\Users\Public\Transcripts\

3. Comprobar registros AlwaysInstallElevated
## PRIVILEGES


## AUTOMATED ENUMERATION


[[WINPEAS COSAS INTERESANTES]] 

Automated tools can be blocked by AV solutions. If this is the case, we can apply techniques learned in the Module "Antivirus Evasion", try other tools such as Seatbelt2 and JAWS,3 or do the enumeration manually.

## KERNEL EXPLOITS

systeminfo
exploit suggester

## WINDOWS SERVICES

[[BINARY HIJACKING]]
[[DLL HIJACKING]]
[[UNQUOTED SERVICES PATHS]]


## SCHEDULED TASK

Enumeración

```
schtasks /query /fo LIST /v

 Get-ScheduledTask | Where-Object { $_.State -ne 'Disabled' }

# Miramos los permisos y si podemos escribir en el direcotrio y tenemos privilegios sobre ese entonces lo modificamos

cacls C:\Users\steve\Pictures\BackendCacheCleanup.exe
```

Para filtar la salida y buscar una ejecucion cercana usar un fichero de texto:

![[Pasted image 20230523195955.png]]

```
type output.txt | find "5/23/2023" | find "Next "
```