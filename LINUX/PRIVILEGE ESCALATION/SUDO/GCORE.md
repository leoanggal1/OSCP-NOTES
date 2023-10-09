## DESCRIPTION

PERMITE LEER INFORMACION DE UN PROCESO EN CONCRETO

![[Pasted image 20230706140234.png]]

#### Mas información
* https://gtfobins.github.io/gtfobins/gcore/


## EXPLOITATION

1. Buscar el proceso que puede tener información

```

ps -ef | grep passw

```

![[Pasted image 20230706140403.png]]
2. Lo usamos para strar las strings
```
sudo /usr/bin/gcore 527
```

![[Pasted image 20230706140430.png]]

![[Pasted image 20230706140336.png]]
## MACHINES

* Hack The Box: 
* PG: Pelican

**!!NOTA IMPORTANTE!!** 