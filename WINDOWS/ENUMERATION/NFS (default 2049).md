## DESCRIPTION

Enumeramos con nmap o con rpcinfo y vemos que tiene abierto el puerto de [[RPC (135)]] y el de NFS. Por lo que es lógico pensar que tiene algun directorio montado/compartido.

![[Pasted image 20230228210940.png]]

![[Pasted image 20230228210839.png]]


#### Mas información
* https://book.hacktricks.xyz/network-services-pentesting/nfs-service-pentesting
* https://0xdf.gitlab.io/2020/09/05/htb-remote.html#shell-as-iis

## EXPLOITATION

1. Enumerar directorios compartidos:

```
showmount -e <<IP>>

mount -t nfs [-o vers=2] <ip>:<remote_folder> <local_folder> -o nolock

#Ejemplo
mkdir /mnt/new_back
mount -t nfs [-o vers=2] 10.12.0.150:/backup /mnt/new_back -o nolock
```

**!!NOTA IMPORTANTE!!** 
	You should specify to **use version 2** because it doesn't have **any** **authentication** or **authorization**.

## MACHINES

* Hack The Box: Remote
