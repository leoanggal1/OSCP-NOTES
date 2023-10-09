

PRERREQUISITES --> CHECKTOOLS:

```
which nmap aws nc ncat netcat nc.traditional wget curl ping gcc g++ make gdb base64 socat python python2 python3 python2.7 python2.6 python3.6 python3.7 gcc perl php ruby xterm doas sudo fetch docker lxc ctr runc rkt kubectl 2>/dev/null
```

1.   KERNEL

```
uname -a
lsb_release
```

2. GROUP

```
id
```

* Buscar ficheros que tengan el permiso de un grupo en concreto

```
find / -group “admin” -ls 2>/dev/null
```

* Grupos interesantes: lxd, docker, sudo, adm, staff, admin...

* Ver variables de entorno `env` y en `.bashrc`  

* MIRAR CREDENCIALES EN WP-CONFIG: wp-config.php

* Lxd, docker --> buscar exploit

3. SUDO

```
sudo -l
```

Probar si tenemos permisos

```
sudo su
sudo -i
```

Utilizar --> https://gtfobins.github.io/

4. SUID 

```
find / -perm -4000 2>/dev/null
```

Utilizar --> https://gtfobins.github.io/

* **¡¡NOTA IMPORTANTE!!** : pkexec  --> PWNKIT

5. HISTORIAL

```
history
```

6. CAPABILITIES

```
getcap -r / 2>/dev/null
```

7. USUARIOS

```
cat /etc/passwd
```

8. PERMISOS PASSWD

```
ls -l /etc/passwd
```

9.  MIRAR FICHEROS DE CONFIGURACIÓN

```
#Ejemplo 1: /var/www
```

10.  PROCESOS Y PUERTOS ABIERTOS

```
ps aux
netstat -atunp
ss -anp
lsof
```

* Importante mirar si hay servicios web internos [[INTERNAL WEB SERVER]]

1. SUDO VERSION

```
# Menores de la 
sudo -V | grep "Sudo ver" | grep "1\.[01234567]\.[0-9]\+\|1\.8\.1[0-9]\*\|1\.8\.2[01234567]"
```

BUSCAR CONTRASEÑAS EN PROCESOS EN TIEMPO REAL

```
sudo tcpdump -i lo -A | grep "pass"
watch -n 1 "ps -aux | grep pass"
```

12. TAREAS PROGRAMADAS

```
cat /etc/crontab; crontab -l; cat var/spool/cron/crontabs
grep "CRON" /var/log/syslog
ls -lah /etc/cron*
crontab -l
pyspy
```

13. CLAVES id_rsa

```
find / -name id_rsa 2>/dev/null
```

14. EDITABLE FILES

```
find / -writable ! -user ‘whoami’ -type f ! path “/proc” ! -path “/sys/”

find / -writable -type d 2>/dev/null
```

15. ARE YOU LOST?

```
Linpeas.sh
linenum.sh
unix-privesc-check
```

16. ENUMERATE DIRECTORIES

	For example: /mnt /opt/ /media

17. BUSCAR FICHEROS INTERESANTES

	For example: backup, txt, elementos borrados, steganografía, etc.