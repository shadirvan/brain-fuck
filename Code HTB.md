```
──(kali㉿kali)-[~]
└─$ nmap -sV 10.10.11.62             
Starting Nmap 7.95 ( https://nmap.org ) at 2025-07-27 06:29 EDT
Nmap scan report for 10.10.11.62
Host is up (0.64s latency).
Not shown: 998 closed tcp ports (reset)
PORT     STATE SERVICE VERSION
22/tcp   open  ssh     OpenSSH 8.2p1 Ubuntu 4ubuntu0.12 (Ubuntu Linux; protocol 2.0)
5000/tcp open  http    Gunicorn 20.0.4
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 22.30 seconds

```

- The port 5000 is open and running Gunicorn 20.0.4
- visiting the website gives a code editor
- some of the keywords are restricted,  like import, os, subprocess this prevent from accessing the shell.
- there are option to run and save the codes.