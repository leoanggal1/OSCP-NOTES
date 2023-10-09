## DESCRIPTION

Each Windows service has an associated binary file. These binary files are executed when the service is started or transitioned into a running state.

For this section, let's consider a scenario in which a software developer creates a program and installs an application as a Windows service. During the installation, the developer does not secure the permissions of the program, allowing full Read and Write access to all members of the Users group. As a result, a lower-privileged user could replace the program with a malicious one. To execute the replaced binary, the user can restart the service or, in case the service is configured to start automatically, reboot the machine. Once the service is restarted, the malicious binary will be executed with the privileges of the service, such as _LocalSystem_.


Enumeración de procesos running:

```
Get-CimInstance -ClassName win32_service | Select Name,State,PathName | Where-Object {$_.State -like 'Running'}
```

**!!NOTA IMPORTANTE!!** 
* When using a network logon such as WinRM or a bind shell, Get-CimInstance and Get-Service will result in a "permission denied" error when querying for services with a non-administrative user. Using an interactive logon such as RDP solves this problem.

#### Mas información
* https://github.com/nickvourd/Windows_Privilege_Escalation_CheatSheet


## EXPLOITATION

### OPTION 1: Restarting a Service

1. Encontramos un ejecutable con full access (al directorio y al propio ejecutable).

![[Pasted image 20230413182323.png]]
2. Creamos una reverse shell y lo subimos al mismo directorio (suplantandolo).

3. Nos ponemos a la escucha.

4. Resetamos el servicio y comprobamos si obtenemos la shell (si no podemos resetear la máquina si tenemos permisos y comprobamos si se inicia en el reinicio)

![[Pasted image 20230413182344.png]]

![[Pasted image 20230413182354.png]]

### OPTION 2: TAREA PROGRAMADA

1. Encontramos un ejecutable con full access (al directorio y al propio ejecutable) y encima comprobamos que se ejecuta al inicio.
2. Enumeramos los ejecutables que se ejecutan periodicamente (es posible que no tengamos permisos para ver esto, pero un backup o algo recurrente podría ejecutarse en 2 plano)
3. Creamos una shell, sustituimos el ejecutable y nos ponemos a la escucha. Pasado un tiempo se conectará, ver MAS INFORMACION.
Mirar ejemplo [[EXE TAREA PROGRAMADA]]

### OPTION 3: APAGAR LA MAQUINA

1. Encontramos un ejecutable con full access (al directorio y al propio ejecutable) y encima comprobamos que se ejecuta al inicio.
```
 Get-CimInstance -ClassName win32_service | Select Name, StartMode | Where-Object {$_.Name -like 'BackupMonitor'}
```
![[Pasted image 20230522193636.png]]

3. Comprobamos que tenemos permiso para apagar la mauqina:
![[Pasted image 20230413182512.png]]
3. Reseteamos la maquina

```
shutdown /r /t 0
```

## MACHINES

* Hack The Box: 


**!!NOTA IMPORTANTE!!** 