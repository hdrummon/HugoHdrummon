---
title: "Reflection4"
date: 2020-02-10T21:11:05+11:00
description: "Reflection for fourth sprint"
displayInLine: true
displayInMenu: false
draft: false
---

### Personal Reflection 4
Overall this week was quite busy in terms of content. It introduced me to new concepts while also challenging my existing knowledge of Pen-Testing. The boxes that I did were quite challenging since I’m more used to smaller tasks on CTFs rather than enumeration, exploitation and escalation in box pen-testing.
Unfortunately there was a major issue that stopped me from completing my submission box, which I hope to resolve for next week. I was quite content about how this week went, but I intend to complete the unfinished box once I fix my WPScan.

## Monday 10/02
Again I was slightly late to the session due to my other subject **Career Management for IT Professionals Summer (31016)** having to do a 30 minute presentation for our final assignment. So I missed the stand-up meeting and the beginning of Jasons 
demonstration on the Wakanda box. While I was initially late, I still attempted to understand how the progress came up to this point by understanding what the overall goal was. From my understanding, it was to work your way from surface level information
and slowly make way to gain control of root.
<figure>
<img src="/img/Wakanda.png" >
<figcaption>
*Very general notes on Wakanda box*
</figcaption>
</figure>
While some of the concepts I’m familiar with. It is the overall process and actually knowing what appropriate steps to take that I wish to understand.
We were then told what our next deliverable will be, that being a write-up of our own attempt at a penetrate a box challenge and documenting the process. In order to prepare for this deliverable, I have attempted the **Basic Pen-Testing 1** challenge in 
order to get familiar with the process necessary to work my way through it from the surface. I managed to complete it in class but plan on creating a Write-up and re attempting it tomorrow to refresh myself.

## Tuesday 11/02 Wednesday 12/02
Both Tuesday and Wednesday was spend mostly on doing Write-Ups and attempts on 2 machines. Primarily **<a href="https://www.hdrummon.me/post/write-ups/basic-penetration-testing-1-write-up/">** Basic Pen-Testing</a> and **<a href="https://www.hdrummon.me/post/write-ups/me-and-my-girlfriend-write-up-1/">** Me and My Girlfriend</a> machines. They were quite challenging considering it forced me into concepts I’m not familiar with
such as reverse shell and privilege escalation.
<figure>
<img src="/img/PrivEsc.png" >
<figcaption>
*Explination of Privilage Escalation on Hacksplaining*
</figcaption>
</figure>
They are interesting concepts but have a lot behind them but are vital for most boot-to-root exercises.
I did receive feedback regarding my Reflection 3 which required a couple more artefacts to support my sprint. This is mostly my own issue as I didn’t anticipate that I would require more information to meet the requirements of the week. As a result I
plan on fleshing out my reflections in a lot more depth while also remaining in the borders of what is required of me.
<figure>
<img src="/img/feedback.png" >
<figcaption>
*Explination of Privilage Escalation on Hacksplaining*
</figcaption>
</figure>

## Thursday 13/02
Today was primarily focused on boot-to-root challenges and selecting my box that I need to hack for our submission. Since the **Me and My Girlfriend box** was done by another student, I decided to find a slightly more challenging box to do.
The box selected was **Literally-Vulnerability** box, which has 3 flags within the machine (local.txt, user.txt, root.txt). 
<figure>
<img src="/img/Literally_vul_desc.png" >
<figcaption>
*Description of the box on VulHub*
</figcaption>
</figure>
Before Jason did a demonstration of a boot-to-root we did another stand up regarding out strengths and weaknesses.
I primarily focused on my slow but steady adaptation to the process of analysing a machine and penetrate it. As for weaknesses its mostly being able to recognize the vulnerabilities a machine has and the steps to exploit it. I hope to solve this by just continuing to
get to root on different challenges.

I then did a 1-on-1 feedback regarding my Reflection 3, and what changes I need to submit it as a pass. The primary changes needed are just having artefacts for team collaboration and providing evidence on my technical knowledge of SQL Injections. 
Aside from that I received feedback about my presentation which was apparently good overall. Once I knew what changes I needed for my reflection 3, I’ve made the changes and posted some screenshots supporting these statements.
For the rest of the day I spent on creating a section on my portfolio for Write-Ups and for my submission this Sunday.


## Friday 14/02 Sunday 16/02
The last couple of days of the week were primarily focused on boot-to-root with my selected box being **Literally-Vulnerability**. This was quite a challenging box compared to **Basic Pen-Testing1** and **Me and My Girlfriend1**.
There was a major error that prevented me from continuing the box which in turn halted my writeup for the box. I was left seriously frustrated with how this may impact me and the dissatisfaction of not being able to completely attempt the box.
I even contacted Jason about this issue and Nik who is also doing the same box as me. Nik also had the same issue and the suggestions that Jason made didn’t work as it continued to error. 
<figure>
<img src="/img/nik.png" >
<figcaption>
*Screenshot with Nik about the same WPScan issue*
</figcaption>
I was also preparing for a presentation with Dylan for our other subject,
**Career Management for IT Professionals Summer (31016)**. This really tested my management skills having to manage both preparing with my team for that presentation and conducting my write-up / trouble shooting my **WPScan** issue.


## Issues
As mentioned, a huge issue this sprint was the **WPScan** issue that impeded my progress on the **Literally-Vulnerability** box. During the progress of the box, I came to a section that enabled me to do a **WPScan** on the website to detect other users. 
Every time I attempt to scan the websites IP and port I kept getting the same error message. Even when attempting to update the tool I receive the same error.
<figure>
<img src="/img/WPScan.png" >
<figcaption>
*WPScan error on update*
</figcaption>
</figure>
I attempted to troubleshoot the error, hardly anything tangible. I spoke with Nik who is doing the same box and also encountered the same issue, but neither of us had any knowledge to fix this issue.
I then also contacted Jason about the issue, mostly discussed other options like alternative enumeration methods and updating. Sadly neither of which held any results. And with Nik also having the same issue, hopefully Nik and myself can resolve the issue in class.
<figure>
<img src="/img/nik.png" >
<figcaption>
*Screenshot with Nik about the same WPScan issue*
</figcaption>
</figure>
<figure>
<img src="/img/JasonChat.png" >
<figcaption>
*Screenshot of my chat with Jason discussing the issue*
</figcaption>
</figure>
Apart from that, the only other issue is that I didn't interact with any stakeholders or find any particular issue in the industry. I intend to improve on this by being more engaging next week and researching 
into current industry problems that I can discuss, that I would also understand and relate to my study in some way.
<figure>
<img src="/img/JasonChat2.png" >
<figcaption>
*Screenshot of my chat with Jason discussing my lack of communication with stakeholders*
</figcaption>
</figure>
## Goals/ To-do list
- ~Try to do more wargames and improve write ups.~
- Improve time management techniques.
- Improve team management and communication.
- Improve and make changes to website (background / presentation).
- Learn more about Git and Hugo to better edit my site.
- Understand the process of procedures in web pen-testing.
- Fix Kali **WPScan** issue > Finish **Literally-Vulnerability** box.
