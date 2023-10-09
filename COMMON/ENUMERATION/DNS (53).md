
## DESCRIPTION
The Domain Name Systems (DNS) is the phonebook of the Internet. Humans access information online through domain names, like nytimes.com or espn.com. Web browsers interact through Internet Protocol (IP) addresses. DNS translates domain names to [IP addresses](https://www.cloudflare.com/learning/dns/glossary/what-is-my-ip-address/) so browsers can load Internet resources.


#### Mas información
* https://book.hacktricks.xyz/network-services-pentesting/pentesting-dns

## EXPLOITATION

```
# 1 Enumeración con dig, BUESCA SUBDOMINIOS

dig axfr friendzone.red @10.10.10.123

# 2 Enumeración con host

host -l cronos.htb 10.10.10.13 

#Enumeración con nslookup

 nslookup <<IP>>

whois offensive-security.com -h 192.168.206.251
```

Nos pueden mostrar mas dominios que desconociamos
![[Pasted image 20230316182050.png]]

Para enumerar dominios en función de una lista:

```
for ip in $(cat list.txt); do host $ip.megacorpone.com; done
```

## MACHINES

* Hack The Box: Cronos, 

**!!NOTA IMPORTANTE!!** 