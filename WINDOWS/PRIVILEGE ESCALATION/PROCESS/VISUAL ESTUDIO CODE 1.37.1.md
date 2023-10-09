
## DESCRIPTION

### CVE-2019-1414

The vulnerability allows a local user to escalate privileges on the system.

The vulnerability exists due to an error in Visual Studio Code Visual Studio Code. A local user can run a specially crafted application to inject and execute arbitrary code on the system in context of the current user.

An elevation of privilege vulnerability exists in Visual Studio Code when it exposes a debug listener to users of a local computer, aka 'Visual Studio Code Elevation of Privilege Vulnerability'.

Ejemplo de enumeración en una máquina estaba el proceso Code.

![[Pasted image 20230222192625.png]]

Vemos donde esta los ficheros y buscamos el binario en /bin:

![[Pasted image 20230222192742.png]]

![[Pasted image 20230222192801.png]]

#### Mas información
* https://0xdf.gitlab.io/2020/09/19/htb-multimaster.html
* https://github.com/qazbnm456/awesome-cve-poc#cve-2019-1414
* Tool to download: https://github.com/taviso/cefdebug

## EXPLOITATION

1. Descargamos la tool necesaria de: https://github.com/taviso/cefdebug , en la Kali está en /home/kali/Downloads/cefdebug

2. La subimos a la máquina víctima [[TRANSFERRING FILES]]

3. Lo ejecutamos y nos va a decir si hay algun debuger activo:

```
./cefdebug.exe
```

4. Nos conectamos usando el parametro --url y podemos ejecutar comandos

```
process.mainModule.require('child_process').exec('calc')
```

4. Subimos netcat o Invoke-PowershellTcp y ejecutamos una reverse shell.

## MACHINES

* Hack The Box: Multimaster

**!!NOTA IMPORTANTE!!** 