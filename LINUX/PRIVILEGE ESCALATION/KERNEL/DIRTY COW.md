
## DESCRIPTION
A race condition was found in the way the Linux kernel's memory subsystem handled the copy-on-write (COW) breakage of private read-only memory mappings. All the information we have so far is included in this page.
The bug has existed since around 2.6.22 (released in 2007) and was fixed on Oct 18, 2016. 

MAS INFORMACIÓN: https://github.com/dirtycow/dirtycow.github.io/wiki/VulnerabilityDetails

RECONOCIMIENTO:
Lista de versiones vulnerables:https://github.com/dirtycow/dirtycow.github.io/wiki/Patched-Kernel-Versions

![[Pasted image 20230606182659.png]]

• uname -r
![[Pasted image 20230606182713.png]]

Se puede decir que para todos los sistemas operativos linux muy antiguos es vulnerable.

#### Mas información
* https://github.com/firefart/dirtycow


## EXPLOITATION
Explotación muy facil siguiendo el código de la siguiente Poc (en este caso se añade un usuario con privilegios de root al sistema pero existen otras muchas formas) → Todas las POCS disponibles → https://github.com/dirtycow/dirtycow.github.io/wiki/PoCs 

1º copiamos el script → https://github.com/FireFart/dirtycow/blob/master/dirty.c
2º damos permisos
3º compilamos
![[Pasted image 20230606182728.png]]

Accedemos con el usuario creado: su firefart y la contraseña puesta
![[Pasted image 20230606182732.png]]

## MACHINES

* Hack The Box: Zenphoto

**!!NOTA IMPORTANTE!!** 