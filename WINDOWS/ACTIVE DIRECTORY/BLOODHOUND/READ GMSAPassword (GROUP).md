## DESCRIPTION

Group Managed Service Accounts Overview (GMSA) es cuenta de servicio administrada independiente (sMSA) es una cuenta de dominio administrada que proporciona administración automática de contraseñas, administración simplificada de nombres de entidad de seguridad de servicio (SPN) y la capacidad de delegar la administración a otros administradores.

The attacker can then read the gMSA (group managed service accounts) password of the account if those requirements are met.

Podemos comprobar que somos una cuenta de GSMA con Bloodhound.
![[Pasted image 20230303201759.png]]

#### Mas información
* https://www.thehacker.recipes/ad/movement/dacl/readgmsapassword


## EXPLOITATION

### OPTION 1: LINUX

1. Descargamos la herramienta gMSADumper: https://github.com/micahvandeusen/gMSADumper

2. Ejecutamos la herramienta

```
python3 gMSADumper.py -u <<USER>> -p <<PASSWORD>> -l <<MAQUINA>> -d <<DOMAIN>>

#Ejemplo
 python3 gMSADumper.py -u ted.graves -p Mr.Teddy -l intelligence.htb -d intelligence.htb
```

3. Obtenemos los hashes del usuario sobre el que tenegamos el privilegio.

![[Pasted image 20230303202023.png]]

Obtenemos el hash → svc_int$:::664d14e5f79b09a4a8e39ea52a450cd6


SI TENEMOS ADEMAS EL PRIVILEGIO DE ALOW TO DELEGATE → BINGO → PODEMOS CONSTRUIR UN TICKET IMPERSONANDO A ALGUN USUARIO

### OPTION 2: DESDE WINDOWS


PROCEDIMIENTO:  https://www.thehacker.recipes/ad/movement/dacl/readgmsapassword

![[Pasted image 20230303201120.png]]

OPCION 2 USANDO GMSAPASSWORD READER

Descargar el binario desde aqui: https://github.com/expl0itabl3/Toolies

```
.\GMSAPasswordReader.exe --AccountName 'svc_apache$'
```

![[Pasted image 20230627162621.png]]

#### Nota importante
El rc4_hmac es igual que el hash NTLM -> Ejecución directa

![[Pasted image 20230627162921.png]]

## MACHINES

* Hack The Box: Intelligence
* PG: Heist