
## DESCRIPTION

Si se tiene habilitado el AutoLogon, se puede mirar en el registro para intentar obtener las credenciales del usuario.

#### Mas información
* https://0xdf.gitlab.io/2020/07/18/htb-sauna.html

## EXPLOITATION

* WinPEAS te lo muestra:

![[Pasted image 20230311173812.png]]

* Puedes comprobarlo manualmente:

```
Get-Item -Path Registry::'HKEY_LOCAL_MACHINE\software\microsoft\windows nt\currentversion\winlogon'
```

![[Pasted image 20230311174541.png]]

**!!NOTA IMPORTANTE!!**
* Cuidado con el usuario puede no coincidir -> usar  `net users` 

![[Pasted image 20230311174625.png]]

## MACHINES

* Hack The Box: Sauna
