
## DESCRIPTION

Si encontramos un directorio de GIT, podemos enumerar las commits para ver si se han realizado cambios importantes: contraseñas, exploits, etc.

Encontramos que tienen instalado git en  `C:\Program Files\Git\`  --> Entonces tenemos que buscar un directorio donde tienen el repositorio

#### Mas información
* https://linuxhint.com/what-is-git-commit-id/
* MUY BUENA: 
* https://education.github.com/git-cheat-sheet-education.pdf


## EXPLOITATION

### OPTION 1: ENUMERAR COMMITS 

1. Encontramos un directorio de sincronizado con GIT:

![[Pasted image 20230427132735.png]]

2. Si nos da este error, podemos solventarlo con el comando que nos indica
![[Pasted image 20230427132820.png]]

```
git show -s

#OPCIONAL SI NOS DA ESTE ERROR
git config --global --add safe.directory C:/staging
```

3. Vemos los commint:

![[Pasted image 20230427133018.png]]

```
git log
```

4. Accedemos a la última commit :

```
git show 8b430c17c16e6c0515e49c4eafdd129f719fde74
```

![[Pasted image 20230427133133.png]]

5. Vemos que enocntramos una clave en un cambio que se hizo en un commit.

## MACHINES

* Hack The Box: 


