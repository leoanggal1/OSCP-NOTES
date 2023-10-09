
## DESCRIPTION
**Squid** is a caching and forwarding HTTP web proxy. It has a wide variety of uses, including speeding up a web server by caching repeated requests, caching web, DNS and other computer network lookups for a group of people sharing network resources, and aiding security by filtering traffic. Although primarily used for HTTP and FTP, Squid includes limited support for several other protocols including Internet Gopher, SSL, TLS and HTTPS. Squid does not support the SOCKS protocol, unlike Privoxy, with which Squid can be used in order to provide SOCKS support. (From [here](https://en.wikipedia.org/wiki/Squid_(software))).


#### Mas información
* https://book.hacktricks.xyz/network-services-pentesting/3128-pentesting-squid


## EXPLOITATION



SPOSE Scanner[](#spose-scanner)

Alternatively, the Squid Pivoting Open Port Scanner ([spose.py](https://github.com/aancw/spose)) can be used.

```
python spose.py --proxy http://10.10.11.131:3128 --target 10.10.11.131
```

![[Pasted image 20230701162950.png]]


Utilizamos foxyproxy para acceder al directorio web:

![[Pasted image 20230701163019.png]]

## MACHINES

* Hack The Box: 

**!!NOTA IMPORTANTE!!** 