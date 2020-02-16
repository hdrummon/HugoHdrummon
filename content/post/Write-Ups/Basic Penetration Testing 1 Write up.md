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

I first login as guest since I dont have the password yet and then check the IP of the Pen test VM by inputting the command 

    ifconfig

This will tell me the IP so that I can ping it from the kali machine.

<figure>
<img src="/img/Basic.png" >
<figcaption>
*Using ifconfig to check network settings
</figcaption>
</figure>

<figure>
<img src="/img/Basic1.png" >
<figcaption>
*Ping to check connection*
</figcaption>
</figure>

Now that I know the IP and that its able to connect I can begin scanning for vulnerabilities.

We will use **NMAP** to scan the ports of the pen test VM. we use the following command

    nmap -sV -sC -o pentest.log 192.168.234.129

<figure>
<img src="/img/Basic2.png" >
<figcaption>
*Result of NMAP scan*
</figcaption>
</figure>

I notice that one of the versions for port 21 that's open has ProFTPD 1.3.3c. I look into this by searching it up.

<figure>
<img src="/img/Basic3.png" >
<figcaption>
*Search result of ProFTPD 1.3.3c exploit*
</figcaption>
</figure>

As expected there's an exploit for this service. Now that I know that there's an exploit. I can now find a means of using it.

<figure>
<img src="/img/Basic4.png" >
<figcaption>
*Metasploit exploite for ProFTPD 1.3.3c*
</figcaption>
</figure>

So just from the first link of the search, I found a potential set of commands for **Metasploit.** 

<figure>
<img src="/img/Basic5.png" >
<figcaption>
*Configuring exploit on Metasploit with error*
</figcaption>
</figure>

I ended up encountering an error relating RHOST so I attempted to add the target as the host as well which still resulted in an error. So instead I set the **RHOST** as the IP of the pentest machine and the target as 0. As a result, when executing the exploit it managed to work

<figure>
<img src="/img/Basic6.png" >
<figcaption>
*Proper configuration and execution on Metasploit*
</figcaption>
</figure>

To confirm where I am and what permission I am I ran the **ls** and **whoami** command

<figure>
<img src="/img/Basic7.png" >
<figcaption>
*View directory and what user I am*
</figcaption>
</figure>

As a result, I now have root access.

Now I will take this a step further and determine the login password for the account.

I need to find out where the password would be located, this would be in the /etc/shadow file and as I inspected it is.

<figure>
<img src="/img/Basic8.png" >
<figcaption>
*Contents of /etc/shadow*
</figcaption>
</figure>

Now I’ve found marlinspikes password encrypted, I need to find out what encryption format it is to decrypt it.

After numerous trial and error with other decryption formats, I looked up the password and found people to use John the Ripper to decrypt the password. I exported the password into a local file called **john.txt.** Messing with the formats I used the following command to decrypt the password

    john encoding=raw john.txt

<figure>
<img src="/img/Basic9.png" >
<figcaption>
*Using John the Ripper to determine password*
</figcaption>
</figure>

As a result, the password for marlinspike is in fact "marlinspike".

I confirmed this by exiting the guest session and logging in to the account.
