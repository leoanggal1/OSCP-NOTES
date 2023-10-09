
## DESCRIPTION

Acceder a un puerto interno en otra máquina, como si estuvieras en local

#### Mas información
*  https://ironhackers.es/en/cheatsheet/port-forwarding-cheatsheet/
* https://book.hacktricks.xyz/generic-methodologies-and-resources/tunneling-and-port-forwarding#reverse-port-forwarding


## EXPLOITATION

### OPTION 1: DESDE KALI UN SOLO PUERTO

```
ssh -L <<PUERTO DE NUESTRA MÁQUINA DONDE VAMOS A PODER ACCEDER AL REMOTO>>:localhost:<<PUERTO REMOTO DE LA WEB INTERNA>>-i id_ecdsa anita@192.168.166.246 -p 2222     

Ejemplos
ssh jimmy@10.10.10.171 -L 52846:localhost:52846
ssh -L 8001:localhost:8000 -i id_ecdsa anita@192.168.166.246 -p 2222     
```

Usa -N para evitar que se nos abra una shell.

## MACHINES

* Hack The Box: 

**!!NOTA IMPORTANTE!!** 