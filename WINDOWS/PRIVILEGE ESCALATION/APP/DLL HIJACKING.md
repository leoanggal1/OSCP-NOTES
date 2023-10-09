
## DESCRIPTION
First of all, let’s get the definition out of the way. DLL hijacking is, in the broadest sense, **tricking a legitimate/trusted application into loading an arbitrary DLL**. Terms such as _DLL Search Order Hijacking_, _DLL Load Order Hijacking_, _DLL Spoofing_, _DLL Injection_ and _DLL Side-Loading_ are often -mistakenly- used to say the same.

Dll hijacking can be used to **execute** code, obtain **persistence** and **escalate privileges**. From those 3 the **least probable** to find is **privilege escalation** by far. However, as this is part of the privilege escalation section, I will focus on this option. Also, note that independently of the goal, a dll hijacking is perform the in the same way.


#### Mas información
* https://book.hacktricks.xyz/windows-hardening/windows-local-privilege-escalation/dll-hijacking
* https://www.hackplayers.com/2019/11/una-breve-introduccion-al-dll-hijacking.html


## EXPLOITATION

Para enumerarlo existen varias formas, verlo desde el PORCMOC o bien encontrar algun fichero de logs, etc que haga referencia a que le falta una DLL

https://book.hacktricks.xyz/windows-hardening/windows-local-privilege-escalation/dll-hijacking

### OPTION 1: FICHERO DE LOGS

1. Ver sercicios

```
Get-CimInstance -ClassName win32_service | Select Name,State,PathName | Where-Object {$_.State -like 'Running'}
```

Para ver los permisos

```
 icacls .\Documents\BetaServ.exe
```

3. Creamos una dll con msfvenom

4. La subimos y la alojamos en el direcotorio del ejecutable si es posible, si no en alguna carpeta del parh donde tengamos permisos

The consecutive function calls follow the DLL search order from Listing 56, starting with the directory the application is located in and ending with the directories in the _PATH_ environment variable. We can confirm this by displaying the contents of this environment variable with **$env:path** in PowerShell.

```
$env:path
```

6. Reseteamos el sercicion (MUY IMPORTANTE)


```
Restart-Service BetaService
```



## MACHINES

* Hack The Box: 

**!!NOTA IMPORTANTE!!** 