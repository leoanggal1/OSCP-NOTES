## DESCRIPTION



#### Mas información
* 


## EXPLOITATION

**!!NOTA IMPORTANTE!!** 
```
3. Metasploit (autorute):
 run autorute -s 
 
run autoroute -s 192.69.228.0 -n 255.255.255.0
 background
route print


Tras el pivoting se puede: use auxiliary/scanner/portscan/tcp
set PORTS 80, 8080, 445, 21, 22
set RHOSTS 192.69.228.3-10
exploit
 
 
 portfwd add -l 1234 -p 21 -r 192.69.228.3
portfwd list
```


## MACHINES

* Hack The Box: 