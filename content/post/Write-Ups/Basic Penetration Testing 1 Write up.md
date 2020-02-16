---
title: "Basic Penetration Testing 1 Writeup"
date: 2020-02-16T19:09:19+11:00
description: "Writeup for Basic Penetration Testing 1 box"
draft: false
displayInLine: true
displayInMenu: true
draft: false
---

# Basic Penetration Testing 1 Write-up

I begin by making sure that both Virtual Machines are able to connect by doing a ping test and ensuring that both are on the NAT option for networking.

I first check the IP of the Pen test VM by inputting the command 

    ifconfig

This will tell me the ip so that I can ping it from the kali machine.

![Basic%20Penetration%20Testing%201%20Write%20up/Untitled.png](Basic%20Penetration%20Testing%201%20Write%20up/Untitled.png)

![Basic%20Penetration%20Testing%201%20Write%20up/Untitled%201.png](Basic%20Penetration%20Testing%201%20Write%20up/Untitled%201.png)

Now that I know the ip and that its able to connect I can begin scanning for vulnerabilities.

We will use **NMAP** to scan the ports of the pen test vm. we use the following command

    nmap -sV -sC -o pentest.log 192.168.234.129

![Basic%20Penetration%20Testing%201%20Write%20up/Untitled%202.png](Basic%20Penetration%20Testing%201%20Write%20up/Untitled%202.png)

I notice that one of the versions for port 21 that's open has ProFTPD 1.3.3c. I look into this by searching it up.

![Basic%20Penetration%20Testing%201%20Write%20up/Untitled%203.png](Basic%20Penetration%20Testing%201%20Write%20up/Untitled%203.png)

As expected there's an exploit for this service. Now that i know that there's an exploit. I can now find a means of using it.

![Basic%20Penetration%20Testing%201%20Write%20up/Untitled%204.png](Basic%20Penetration%20Testing%201%20Write%20up/Untitled%204.png)

So just from the first link of the search, I found a potential set of commands for **Metasploit.** 

![Basic%20Penetration%20Testing%201%20Write%20up/Untitled%205.png](Basic%20Penetration%20Testing%201%20Write%20up/Untitled%205.png)

I ended up encountering an error relating RHOST so I attempted to add the target as the host as well which still resulted in an error. So instead I set the **RHOST** as the ip of the pentest machine and the target as 0. As a result, when executing the exploit it managed to work

![Basic%20Penetration%20Testing%201%20Write%20up/Untitled%206.png](Basic%20Penetration%20Testing%201%20Write%20up/Untitled%206.png)

To confirm where i am and what permission I am I ran the **ls** and **whoami** command

![Basic%20Penetration%20Testing%201%20Write%20up/Untitled%207.png](Basic%20Penetration%20Testing%201%20Write%20up/Untitled%207.png)

As a result, I now have root access.

Now I will take this a step further and determine the login password for the account.

I need to find out where the password would be located, this would be in the /etc/shadow file and as I inspected it is.

![Basic%20Penetration%20Testing%201%20Write%20up/Untitled%208.png](Basic%20Penetration%20Testing%201%20Write%20up/Untitled%208.png)

Now ive found marlinspikes password encrypted, i need to find out what encryption format it is to decrypt it.

After numerous trial and error with other decryption formats, I looked up the password and found people to use John the Ripper to decrypt the password. I exported the password into a local file called **john.txt.** Messing with the formats I used the following command to decrypt the password

    john encoding=raw john.txt

![Basic%20Penetration%20Testing%201%20Write%20up/Untitled%209.png](Basic%20Penetration%20Testing%201%20Write%20up/Untitled%209.png)

As a result, the password for marlinspike is in fact "marlinspike".

I confirmed this by exiting the guest session and logging in to the account.