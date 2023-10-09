
## DESCRIPTION

Se pueden crear reglas para modificar los diccionarios de contraseñas, por ejemplo añadiendo un caracter al final, etc.

#### Mas información
* https://hashcat.net/wiki/doku.php?id=rule_based_attack


## EXPLOITATION HASCAT

Una regla no es más que un dichero de texto, por ejemplo una regla que añada un 1 al final de cada palabra:

```
echo \$1 > demo.rule
```

si añadimos la c: 	Capitalize the first letter and lower the rest	c	p@ssW0rd	P@ssw0rd

Si ponemos las condiciones en distintas filas se creará un diccionario con las dos entradas de cada una cada una:


Si lo ponemos todo en la misma fila se concatenará



Para visualizar el diccionario con las reglas aplicadas:

```
hashcat -r demo2.rule --stdout demo.txt <<DICCIONARIO>>
```

## EXPLOITATION JOHN

Util para romber claves id_rsa

1. Creamos nuestro fichero de reglas:

```
kali@kali:~/passwordattacks$ cat ssh.rule
[List.Rules:sshRules]
c $1 $3 $7 $!
c $1 $3 $7 $@
c $1 $3 $7 $#
```

2. Lo añadimos al fichero de configuración de john

```
sudo sh -c 'cat /home/kali/passwordattacks/ssh.rule >> /etc/john/john.conf'
```


3. Ejecutamos:

```
john --wordlist=ssh.passwords --rules=sshRules ssh.hash
```


## MACHINES

* Hack The Box: 

**!!NOTA IMPORTANTE!!** 