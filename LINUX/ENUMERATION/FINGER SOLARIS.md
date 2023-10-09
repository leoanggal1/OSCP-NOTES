## DESCRIPTION

FINGUER ES UN PUERTO QUE SIRVE PARA DAR INFORMACION DE LOS USUARIOS CONECTADOS Y POCO MAS

#### Mas información
* https://book.hacktricks.xyz/network-services-pentesting/pentesting-finger


## EXPLOITATION

```
☐ 1º Enumerate coneccted users: finger @<<IP>>
☐ 2º Enumerate a user: finger <<user>>@<<IP>>
☐ 3º You can use the tool finger_user_enum.pl to enumerate using a users dicctionary:  finger-user-enum.pl -U /usr/share/seclists/Usernames/Names/names.txt -t 10.10.10.76
☐ 4º Check if the user are valid. Generally valid users are those who have the date and time.


Note: If you find usernames then you can try bruteforce to crack their paswords. For example, in SSH service.
```


## MACHINES

* Hack The Box: 

