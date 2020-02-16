
---
title: "Literally Vulnerable Writeup"
date: 2020-02-16T19:09:19+11:00
description: "Writeup for Literally Vulnerable box"
draft: false
displayInLine: true
displayInMenu: true
draft: false
---

When loading up the machine, there appears to be nothing other then a Ubuntu login in screen. Since I don't have any information aside from the booted machines login, my first course of action is to determine the IP of the machine.

By using the following command, I am able to determine the IP of the Literally Vulnerable machine by scanning that network.

    netdiscover -r 192.168.220.0
    
    # -r = Range of IP's

<figure>
<img src="/img/Literally_vul_11.png" >
<figcaption>
*Result of the netdiscover command*
</figcaption>
</figure>

As seen, there are 4 IP's detected from the scan, the first and last IP are rolled out since they are the network and broadcast IP respectively. So more than likely the address 192.168.220.157 is the machines IP. This can be confirmed with an NMAP scan using the following command:

    nmap -A 192.168.220.157
    
    # -A = OS detection, version detection, script scanning and traceroute
<figure>
<img src="/img/Literally_vul_1.png" >
<figcaption>
*Result of NMAP scan*
</figcaption>
</figure>

Some of the open ports discovered show some interesting findings, such as port 21 which indicated an FTP service wit a file of "backupPasswords". This might have a key to get into the machine.

I then determine how to get the file from FTP to my local to view the passwords. So the most notable thing about the service is ***FTP Anonymous***, and after searching it up means and FTP archive that has general access. So we just need to retrieve the file. 
<figure>
<img src="/img/Literally_vul_2.png" >
<figcaption>
*Installing FTP and accessing the server*
</figcaption>
</figure>

So I install the standard FTP application and use it to connect to the IP and login as "Anonymous".
<figure>
<img src="/img/ftp.png" >
<figcaption>
*Exported the Passwords*
</figcaption>
</figure>

I then check what's located there which only presents backupPasswords. I then use the **GET** command to send the file locally and then view it. And so the file contains several passwords addressed to Doe. And the text presents that there is "A bunch of passwords below along with your password" so its possibly that one of these passwords will gain access to the machine and other passwords might have a use down the line.

<figure>
<img src="/img/Untitled1.png" >
<figcaption>
*Attempted to use the passwords to SSH to the machine*
</figcaption>
</figure>

I attempted to use these passwords to SSH into Doe, sadly no luck there. Bit of a dead-end but at least I found some passwords. Let’s move onto the website on port 80.

<figure>
<img src="/img/Literally_vul_4.png" >
<figcaption>
*Viewing the website on port 80*
</figcaption>
</figure>

<figure>
<img src="/img/Literally_vul_5.png" >
</figure>

A lot of the links on the website are broken and don't lead anywhere. So my next step is to look in inspector and console for any clues.

<figure>
<img src="/img/Literally_vul_6.png" >
<figcaption>
*Errors in console*
</figcaption>
</figure>

I noticed how there were several errors in console indicating to the source. That the script failed to load from the source. In this case the source is *literally.vulnerable*.

<figure>
<img src="/img/Literally_vul_7.png" >
<figcaption>
*/etc/hosts file entry*
</figcaption>
</figure>

<figure>
<img src="/img/Literally_vul_8.png" >
<figcaption>
*Updated and restored site*
</figcaption>
</figure>

By inputting the domain name in /etc/hosts it is able to retrieve the necessary scripts to run.

Now that I have proper access to the word press website, now I can look around for anymore leads.

Noting comes up, let’s move on and try that other open port. 65535

<figure>
<img src="/img/Literally_vul_9.png" >
<figcaption>
*Default Apache 2 site*
</figcaption>
</figure>
When accessing the port, Im greeted with a default page for Apache2 Ubuntu. 

I then use **Dirb** to find any hidden directories on the IP, the website and default Ubuntu page to find anymore leads and sure enough there was one on the 65535 port.

<figure>
<img src="/img/Literally_vul_10.png" >
<figcaption>
*Dirb command finding hidden Directories*
</figcaption>
</figure>

As seen there is a large quantity of files and subdirectories within the directory /*phpcms*/. To see this folder I entered the directory into the url.

<figure>
<img src="/img/Literally_vul_12.png" >
<figcaption>
*Accessing hidden directory /phpcms/ and its contents*
</figcaption>
</figure>

<figure>
<img src="/img/Literally_vul_13.png" >
</figure>

I then attempt an WPScan of the webpage to find any other users on the website other then "notadmin". 

Its at this point that I cant continue due to a fatal error in WPScan that prevents me from actually scanning for any users.

<figure>
<img src="/img/Literally_vul_14.png" >
<figcaption>
*WPScan errors*
</figcaption>
</figure>

As seen with the image above, not only does it not scan the directory I need done, but it doesn't even scan the port 80 page or even the IP. I attempted to install it to another Virtual Machine to see if that would work but sadly to no result. Searching up the error on google didn't help either, or looking for alternatives. Sadly with this error it prevents me from pushing through the machine.
