
## DESCRIPTION

En determinados casos tenemos que motar un fichero .vhd en nuestro linux, por ejemplo si enumerando nos encontramos un fichero backup:

![[Pasted image 20230413185141.png]]

#### Mas información
* https://0xdf.gitlab.io/2019/09/07/htb-bastion.html


## EXPLOITATION

### OPTION 1: MONTAR UN FICHERO PESADO

SI TIENES QUE DESCARGARLOD E SMB Y PESA MUCHO LO MEJOR ES MONTARLO: A Windows Image Backup is likely to be large and the transfer will be slow (as the note warns). Rather than try to copy it over, I’m going to mount this share to my filesystem.

```
mount -t cifs //10.10.10.134/backups /mnt -o user=,password=
```

### OPTION 1: MONTAR UN FICHERO .VHD

```
guestmount --add 9b9cfbc3-369e-11e9-a17c-806e6f6e6963.vhd --inspector --ro /mnt2/
```

**!!NOTA IMPORTANTE!!** 
* IMPORTANTE SI TENEMOS MONTADO UN BACKUP DE UN WINDOWS COMPLETO → ENUMERAR LA SAM → Se encuentra en el directorio → /Windows/System32/config → Cuando accedemos aun equipo este directorio suele estar bloqueado pero si lo tenemos montado en nuestro linux → no suele haber problemas → utilizamos secretdump para dumpear la SAM → `secretsdump.py -sam SAM -security SECURITY -system SYSTEM LOCAL` → Crackeamos los hashes*

## MACHINES

* Hack The Box: BASTION

