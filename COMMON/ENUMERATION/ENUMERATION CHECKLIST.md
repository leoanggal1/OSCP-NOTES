
1. HOST DISCOVERY: -sn 

Para obtener solo las IP de la salida del comando:
```
cat targets.nmap | awk '/for/ {print $5}' | grep -v 10
```

2. QUICK SCAN:
```
nmap -p- --open -T5 -v -n -sV <<IP>> (-Pn) -oA quick-nmap
```

3. BIG SCAN 1: 
```
nmap -p- --open -v -sC -sV -o nmap -A -T5 <<IP>> (-Pn) -oA big1-nmap
```
+ -iL targets.txt para especificar fichero objetivo

4. BIG SCAN 2: 
```
nmap -p- --open -T5 -v -n -sV -sC -Pn --script vuln <<IP>> -oA big2-nmap
```
+ -iL targets.txt para especificar fichero objetivo

6. UDP SCAN : -sU
```
nmap -sU -sC --top-ports 20 -oA nmap/udp-top20-scripts 10.10.10.116 
```


## Recursos para enumerar
+ https://github.com/jwardsmith/OSCP-Methodology#port-80-443-httphttps