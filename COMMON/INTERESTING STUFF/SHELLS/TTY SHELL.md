
## DESCRIPTION

En un sistema linux se recomienda ejecutar los siguientes comandos para que la reverse shell se vea de forma adecuada y poder utilizar los controles de copiado, pegado, etc.

Para un sistema Windows es recomendable usar la utilidad rlwrap junto con netcat.

## EXPLOITATION

* LINUX:

```
script /dev/null -c bash
 ^Z
stty raw -echo; fg
reset xterm
export SHELL=bash
export TERM=xterm

# Opción con python
python -c 'import pty; pty.spawn("/bin/bash")'
```

+ WINDOWS:

```
rlwrap nc -lvnp <<Puerto a la escucha>>    
```
