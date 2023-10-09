
## DESCRIPTION

Es posible que no tengamos acceso a un fichero, **FLAG** pero quizás tengamos FULL permisos sobre el directorio. Entonces con este FULL permisos podemos darle permiso a la **FLAG** si se encuentra dentro del mismo.

#### Mas información
* https://0xdf.gitlab.io/2018/06/18/htb-chatterbox.html#reading-roottxt

## EXPLOITATION

1. Para ver los permisos de un directorio

```
<<Directorio>> icals
```

2. Comprobamos que tenemos full acceso:

![[Pasted image 20230302201756.png]]

3. Como sabemos que se encuentra la bandera en ese directorio, entonces podemos cambiar el siguiente permiso sobre el fichero poniendo a nuestro usuario con full access.

![[Pasted image 20230302201859.png]]

## MACHINES

* Hack The Box: Chatterbox
