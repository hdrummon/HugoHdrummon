---
title: "Reflection5"
date: 2020-02-23T18:25:26+11:00
description: "Reflection for fifth sprint"
displayInLine: true
displayInMenu: false
draft: false
---
# Reflection 5
This week was quite eventful for all the good reasons. A lot of activity regarding HackTheBox, getting an invite code/ registering and one of the machines that we had to root OpenAdmin. It focused heavily on the Penetration testing side of Cyber Security with a presentation about it from Deloitte.
Overall an enjoyable experience throughout the week.

## Monday 17/02

Monday was quite an eventful day in a better way than last week, we were required to obtain an invite code for Hack the Box to create and account. 
This was lot harder then I first expected even with watching a video about it a couple of weeks ago. Although with the help from Nik we managed to cooperate through the challenge and get the invite code.
 The challenge tested my use of console and inspector, because typically I only use the inspector for CTF or boot-to-roots, but the invite challenge forced me to understand the use of the console and the browser in a good way. 
It also present familiar concepts like encryption formats ROT13 and Base64 which I've used in the past.
<figure>
<img src="/img/Invite.png" >
<figcaption>
*Getting the invite code and able to register to HackTheBox*
</figcaption>
</figure>
Now with the entry into HackTheBox, the main deliverable for this week is to complete one of the boxes  in hack the box. So far I've made minor progress in class for the box OpenAdmin, but will continue to persist throughout the box across the week.

## Tuesday - Wednesday 18 - 19/02

This period was primarily focused on attempting the box while also installing the necessary files on my mac to be able to also run the virtual machine.
I successfully managed to install the required programs such as Fusion while also focusing on attempting the Open Admin Box.

The progress on the box was quite slow and steady, hardly any direction that I could find without some pointers from other people who have completed the step I'm on. 
Usually when I was stuck I would google search the area I'm in or look into other information sources like write-ups to find any leads to continue. 
Some would help but others would lead me to dead ends, which constantly frustrated me during the enumeration process. 
I was quite relieved when I did manage to step into the right direction at any point because it meant that I actually made progress. 
But each time I did do something, id try to understand what I did and why I did it. 


## Thursday 20/02

Today was quite informative as members from Deloitte Pieter Westein and Nathan Jones came in to do a presentation on Penetration testing and for a pen-test box challenge that we attempted. 
The presentation was quite informative about the attributes of Penetration testing, what's involved and some of the different areas of it that I wasn't aware of such as the lengths of red team offensive operations on a client company. 
The idea of a inconspicuous power plug being used as an access port to access the intranet of a company from the inside of their walls is such an unknown and scary subject for me to understand, but also an intriguing and fascinating idea to the extent that security goes through. 
<figure>
<img src="/img/Tools.png" >
<figcaption>
*Example of the Offensive tools used from the presentation*
</figcaption>
</figure>
We then begin to attempt their challenge box, which was really difficult as it presented a medium for enumerating and exploiting which was git repositories.
While I understood the first sections that I’m familiar with such as **Netdiscover** and **NMAP** scanning, it was later on when we encountered the repository files that it became difficult as we were trying to determine the best course of action with these files.
At this point I attempted to revert to a previously committed instance, but this was a lot more difficult than I expected and didn’t end up finishing that task. Overall was really surprised just how intense the box really was but also disappointed for not making sufficient progress.
<figure>
<img src="/img/Deloitte.jfif" >
<figcaption>
*Deloitte Box challenge*
</figcaption>
</figure>

After the presentation I proposed a question to them in regards of human based threats and how they deal with them. 
That being "How do they deal with the human element in threat assessment in penetration testing and what measures would be taken to prevent this". 
As Nathan replied, they typically utilize human threat reconnaissance and employee threat assessment of how they would interact with possible exploits like social engineering or phishing links. 
They then mentioned how there would be blast emails that stress the importance of warning about phishing links and just letting in random people into the building to plant these rogue devices, while also creating incentives to spot protentional threats and rogue security that act in as threats to create awareness. 
This in itself is a smart idea to create incentives to encourage the active observation of threats within an organization. 
This was also a good opportunity to interact with them as stakeholders since I didn’t last sprint, also being that they are active Penetration Testers for Deloitte and have an important insight in the field that I will once need.


The rest of the day was spent attempting the HackTheBox that were using for our deliverable.
As I mentioned in my stand up meeting after the presentation, how I'm slowly understanding the steps necessary in going through these difficult boxes, which then tied into my major weakness which is my distaste towards enumeration and how time consuming it can be to enumerate a potential lead, to only realize its gone nowhere.
 <br>
 That being said, I stated how I wanted to try and attempt to get root in my OpenAdmin box, which in the later hours of the night I finally managed to get Root on OpenAdmin.
 I was extremely relieved and zealous at the idea that I finally managed to root such a difficult box even after finally getting an invite code which has been a long time goal. 
 While I had to get numerous hints to guide me in the right direction because of how lost I was, I was still quite surprised how I managed the box. I was however disappointed how over reliant I was on hints from others, as I knew in the real world hints wouldn't be given out so easily given. 
 <figure>
<img src="/img/Rooted.png" >
<figcaption>
*Submitted user and root flag*
</figcaption>
</figure>

## Friday 21/02

Today was primarily about fleshing out my reflection and preparing for my write up. Once I managed to get root, I attempt to redo the step by step process of how I managed to get to root only mentioning the rabbit holes I had along the way but mostly focus on the straight forward process I experienced with the box. 
As I discuss with Larry and Jason in my 1-on-1 feedback, I just want to make sure that I don't over complicate my responses for my write-up while also not over simplifying my response. 
I also wanted to confirm with Jason as well about how I would submit my write-up for OpenAdmin without displaying the User.txt and Root.txt on the page (Which you can find the write-up here protected with the hash of Root).
<figure>
<img src="/img/JasonWriteup.png" >
<figcaption>
*Disussion I had with Jason regarding submission of the completed Write-up*
</figcaption>
</figure>

## Issues
Primarily, the biggest issue I faced in this deliverable was my over reliance on help from others. This really inhibited my overall understanding and my progress during the enumeration process.
This mostly ties into time management as enumerating is a lengthy process and with a combination of my shear laziness and poor time management skills really affected how I performed. Although I managed to get root, it wasn’t without help from others.
I hope to change this however by enforcing strict management regarding my time and persevering through the enumeration process.  
 
## Goals/ To-do list
- Improve time management techniques.
- ~Improve team management and communication.~
- Improve and make changes to website (background / presentation).
- Learn more about Git and Hugo to better edit my site.
- ~Understand the process of procedures in web pen-testing.~
- Fix Kali **WPScan** issue > Finish **Literally-Vulnerability** box.