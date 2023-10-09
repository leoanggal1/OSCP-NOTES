## DESCRIPTION

mRemoteNG is a remote connection management tool, and it allows the user to save passwords for various types of connections. There is a file in the user’s AppData directory, **confCons.xml**, that holds that information.

Es una herramienta para gestionar conexiones remotas, por lo que tiene que almacenar las claves de estas conexiones. Las suele almacenar en el fichero confCons.xml y existe una vulnerabilidad que permite DESENCRIPTARLAS.

#### Mas información
* https://0xdf.gitlab.io/2019/09/07/htb-bastion.html#privesc-to-administrator

## EXPLOITATION

1. Si vemos en `C:\Program Files (x86)` o en otro directorio que tiene mRemoteNG, entonces debemos de buscar el archivo que contien las contraseñas `confCons.xml`.
![[Pasted image 20230303170517.png]]

2. Suele encontrarse en `C:\Users\L4mpje\AppData\Roaming\mRemoteNG` pero puedes buscarlo con [[WINDOWS/ENUMERATION/BÚSQUEDA]]

![[Pasted image 20230303170656.png]]

![[Pasted image 20230303170944.png]]

3. Ecxisten varias técnicas para desencriptar las claves -> ver https://0xdf.gitlab.io/2019/09/07/htb-bastion.html#privesc-to-administrator

4. Mejor opción utilizar la siguiente herramienta: https://github.com/kmahyyg/mremoteng-decrypt

```
python3 mremoteng_decrypt.py -s "aEWNFV5uGcjUHF0uS17QTdT9kVqtKCPeoC0Nw5dmaPFjNQ2kt/zO5xDqE4HdVmHAowVRdC7emf7lWWA10dQKiw==" 
```

![[Pasted image 20230303170928.png]]
## MACHINES

* Hack The Box: Bastion

