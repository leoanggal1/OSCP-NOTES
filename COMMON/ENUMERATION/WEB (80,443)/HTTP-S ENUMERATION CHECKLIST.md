
* View Web App and Wappalizer
* Mirar version CMS → exploit
* Directory Enumeration (MIRAR EN TODOS LOS DIRECTORIOS ENCONTRADOS)
      1. nmap --script http-enum <<IP>>
      2. gobuster dir -w /usr/share/wordlists/dirb/common.txt -t 80 -u <<IP>>

* Parameter fuzzing with wfuzz
      1. wfuzz -c --hc=404 -z file,/usr/share/wordlists/wfuzz/webservices/ws-dirs.txt <<IP>>  
      PARA BUSCAR FICHEROS CON INFORMACIÓN SENSIBLE SIN QUE LLEVE MUCHO TIEMPO PUEDES USAR ESTE DICCIONARIO (POR EJEMPLO PARA LOS .TXT) → cat /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-medium.txt | grep -iE "user|pass|key|database"
      6. wuzzing -> dominios > wfuzz -c -f subdomains.txt -w /usr/share/wordlists/SecLists/Discovery/DNS/bitquark-subdomains-top100000.txt -u "http://shoppy.htb/" -H "Host: FUZZ.shoppy.htb" --hl 7
      7. fuzzing ficheros con extensiones típicas → -u http://love.htb -x php -w /usr/share/seclists/Discovery/Web-Content/raft-medium-directories-lowercase.txt 


* SI HAY ALGÚN /CGI-BIN/ → Check Shell Shock (cgi-bin/status)
* Check /robots.txt, .htaccess, .htpasswd
* Use Nikto
* View Source code 
* Check HTTP Request with curl (puede que te diga un dns name)
* View Console
* Run Burp Suite
* Check OPTIONS → 
* HTTP PUT / POST File upload → POST: curl http://<IP address> --upload-file test.txt
* Apache version exploit & other base server exploits