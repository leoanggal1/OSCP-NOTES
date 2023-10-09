
## DESCRIPTION

En los registro de putty y ssh se pueden quedar almacenadas credenciales


#### Mas información
* https://book.hacktricks.xyz/windows-hardening/windows-local-privilege-escalation


## EXPLOITATION

Si tenemos el Putty instalado --> comprobar estos registros aunque el WINPEAS NO LO MUESTRE

Putty Creds
```
reg query "HKCU\Software\SimonTatham\PuTTY\Sessions" /s | findstr "HKEY_CURRENT_USER HostName PortNumber UserName PublicKeyFile PortForwardings ConnectionSharing ProxyPassword ProxyUsername"

```

![[Pasted image 20230603190616.png]]

Putty SSH Host Keys

```
reg query HKCU\Software\SimonTatham\PuTTY\SshHostKeys\
```

Tambien SSH Keys in registry

```
reg query HKEY_CURRENT_USER\Software\OpenSSH\Agent\Keys
```

## MACHINES

* Hack The Box: 

**!!NOTA IMPORTANTE!!** 