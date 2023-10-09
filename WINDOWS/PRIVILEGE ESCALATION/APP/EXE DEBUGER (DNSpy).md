## DESCRIPTION

Si tenemos un ejecutable, con alguna clave encriptada o algun dato de interés, entonces recomendamos pasarlo a la máquina linux y usar DNSpy.exe para debuguerarlo y encontrar la clave trás su desencriptado.


#### Mas información
* Video S4vitar support
* Herramienta: https://github.com/dnSpy/dnSpy
* https://0xdf.gitlab.io/2020/07/25/htb-cascade.html

## EXPLOITATION

1. Transferir el fichero a la KALI

2. Conectarte a la VPN con OpenVPN GUI

3. Abrir el .EXE con DNSpy

![[Pasted image 20230321184621.png]]

4. Buscar la función que desencripta la contraseña y poner un punto de parada justo despues:
![[Pasted image 20230321184702.png]]

## MACHINES

* Hack The Box: Support, Cascade

**!!NOTA IMPORTANTE!!** 