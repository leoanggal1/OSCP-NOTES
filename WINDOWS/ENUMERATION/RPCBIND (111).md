
## DESCRIPTION

Portmapper (también conocido como rpcbind, portmap o RPC Portmapper) es un **servicio de llamadas a procedimientos remotos de Open Network Computing** (ONC RPC) que se ejecuta en nodos de red que proporcionan otros servicios de ONC RPC.

Requerido por NFS.

#### Mas información
* https://book.hacktricks.xyz/network-services-pentesting/pentesting-rpcbind

## EXPLOITATION

1. Se puede enumerar con nmap con la opción -sC

2. O usando
```
rpcinfo <<IP>>
```

**!!NOTA IMPORTANTE!!** 
	Prestar atención si hay dicheros compartidos NFS 

## MACHINES

* Hack The Box: Remote
