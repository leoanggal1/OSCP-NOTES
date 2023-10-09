
## DESCRIPTION



#### Mas información
* https://www.ired.team/offensive-security-experiments/active-directory-kerberos-abuse/active-directory-enumeration-with-powerview


## EXPLOITATION

1. La subimos 

```
Import-Module .\PowerView.ps1
```


Nota importante si te dicen que no se puede ejecutar scripts:
![[Pasted image 20230525183239.png]]
Entonces:
```
powershell -ep bypass
```

### OPTION 1: Comandos útiles

```
Get-NetDomain

Get-NetUser

# Seleccionar un atributo por ejemplo cn
Get-NetUser | select cn,pwdlastset,lastlogon


Get-NetGroup | select cn

Get-NetGroup "Sales Department" | select member

#Para obtener informacion de los ordenadores del dominio, versiones,nombre, etc
Get-NetComputer
```


Ver permisos y sesiones

```
Find-LocalAdminAccess

Get-NetSession -ComputerName files04

Ver permisos
Get-Acl -Path
```

Para ver usuarios logged se puede usar la tool PsLoggedon.exe

```
.\PsLoggedon.exe \\web04
```


## MACHINES

* Hack The Box: 

**!!NOTA IMPORTANTE!!** 