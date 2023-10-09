
## DESCRIPTION

Acceder a un puerto interno en otra máquina, como si estuvieras en local

![[Pasted image 20230529193756.png]]

#### Mas información
*  https://ironhackers.es/en/cheatsheet/port-forwarding-cheatsheet/
* https://book.hacktricks.xyz/generic-methodologies-and-resources/tunneling-and-port-forwarding#reverse-port-forwarding


## EXPLOITATION

### EN LA MÁQUINA VICTIMA (LA QUE HACE DE PUENTE)

```
ssh -N -D 0.0.0.0:9999 database_admin@10.4.50.215  
```

Usa -N para evitar que se nos abra una shell.

### EN LA MÁQUINA KALI

![[Pasted image 20231009183732.png]]

Y utilizamos proxychains

```
proxychains smbclient -L //172.16.50.217/ -U hr_admin --
```
## MACHINES

* Hack The Box: 

**!!NOTA IMPORTANTE!!** 