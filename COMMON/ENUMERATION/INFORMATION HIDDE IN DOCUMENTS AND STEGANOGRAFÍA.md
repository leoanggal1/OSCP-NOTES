
## DESCRIPTION



#### Mas información
* 


## EXPLOITATION

### OPTION 1: EXIFTOOL

Para obtener informacion de documentos como pdf:

```
exiftool -a -u brochure.pdf
```

![[Pasted image 20230511195828.png]]

### OPTION 2: STRINGS

```
strings <<file>>
```


### OPTION 3: ESTEGANOGRAFÍA EN IMAGENES

Si tenemos una imagen y una passphrase:
EJEMPLO:
Super elite steg backup pw UPupDOWNdownLRlrBAbaSSss → Esteganografía y tenemos una imagen → la descargamos y usamos la herramienta 

PODEMOS UTILIZAR LA HERRAMIETNA Y OBTENER UNA PASS O ALGUNA INFORMACIÓN IMPORTANTE

Now I’ll try steghide, a command steg tool, with the follow arguments:
extract - I want to extract data
-sf irked.jpg - give the file to extract from
-p - passphrase

![[Pasted image 20230606183005.png]]

Kab6h+m+bbp2J:HG

## MACHINES

* Hack The Box: 

**!!NOTA IMPORTANTE!!** 