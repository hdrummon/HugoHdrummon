---
title: "Reflection3"
date: 2020-02-03T16:55:30+11:00
description: "Reflection for third sprint"
displayInLine: true
displayInMenu: false
draft: false
---

### Personal Reflection 3
Over all this sprint was quite successfully in some areas as I have now attempted and successfully adopted the daily reflection writing. I now have a better idea of how and **SQLInjection** operates on a more theoretical level now and
how it would be prevented though the research done for our presentation. While there are some areas that I still need to cover a bit more such as general web exploits and basic pen-testing operations, I believe that I’m on the right track at the moment.

## Monday 3/02
I arrived slightly late to class due to my other subject **Career Management for IT Professionals Summer (31016)** having mock interviews to prepare us for future application process.
Today began with our stand-up meeting instructed to express our strengths and weaknesses from last week and how we intend to improve and manage our weaknesses. I primarily focused on my time with **Linux CLI** as its always been an area that I closely intend to improve through more often use, and by constantly using **Linux CLI** in CTF challenges, I intend to further improve my **Linux CLI** skills. 
This then leads into a big weakness of mine is further understanding **GIT** and **Hugo** as recently I've had trouble deploying some of the edits for my Reflection2. 
This was primarily due to me forgetting to create the post initially and then coping my text over from notion. This causes a couple of errors and formatting issue but with further research into **Shortcodes** and **Hugo** formatting and proper procedure I should be able to resolve this issue in time.
<figure>
<img src="/img/Reflection2.png" >
<figcaption>
*Using Notepad++ to fix up my Reflection2*
</figcaption>
</figure>
After the stand-up we proceeded to talk about our next deliverable, Web Application attack/exploit. So for this deliverable we are researching **SQL Injection**, what it is, how it works and its impact on the industry as well as what can be done to mitigate it.
My section is primarily focusing on how it works and providing a demo of **SQL Injection** and the logic behind it. This for me is a good opportunity to tackle a problem I've had for a while which is primarily understanding how it actually works, how I will encounter it and most important for me, how to use it for bounties and challenges. 
This stems back to when I first joined the Cyber-Security Society and experienced challenges that involved **SQL Injections**. This will be a great opportunity to finally understand it in greater depth. 
My primary focus for this presentation is providing a demo showing some of the more challenging and insightful elements of SQL Injection. 
Once we decided on what roles we were to present, I then made a Microsoft teams group with my teammates Dowsen and Manish.
<figure>
<img src="/img/Team.png" >
<figcaption>
*Microsoft Team chat made with my group*
</figcaption>
</figure>
<figure>
<img src="/img/Assign.png" >
<figcaption>
*Assigning of roles for the presentation*
</figcaption>
</figure>

## Tuesday 4/02 - Wednesday 5/02
Tuesday and Wednesday I was focused more on find a good example of an **SQL Injection** before the presentation, but then soon side tracked and attempted more OverTheWire. I moved from Bandit to Natas which focused a lot more on web vulnerabilities and exploits. 
I wasn't able to get far only getting to Natas 4 and I plan on re-doing them with a proper write-ups later but was otherwise surprised that I even got this far. As for **SQLInjection** research, Hacksplaining provided a quite easy and understandable explanation of what
the main fundamental concept of an **SQLInjection** was by providing both and interactive demo, and an explanation on what it is and how to prevent it.
<figure>
<img src="/img/SQLI.png" >
<figcaption>
*Hacksplaining Information of an SQL Injection*
</figcaption>
</figure>

I managed to record a demo of an **SQL Injection** from Herokuapp, but I'm still in search of a more complex **SQL Injection** to show how complex and lethal they can be. 
I'm happy with how the demo turned out and I'm continuing to research how **SQL Injections** operate through looking into other CTF challenges.
<figure>
{{< youtube id="BEXI_FpnSpI" autoplay="yes">}}
<figcaption>
*Demonstration of an SQLInjection*
</figcaption>
</figure>
From both the Hacksplaining demo and description as well as other media like Youtube videos and websites, I understand how **SQLInjection** works. It in essence exploits how an SQL query operates by injecting key SQL characters that compile with the query.
They are typically injected into input fields like login or search boxes. These enable attackers to exploit these inputs and inject SQL code with malicious outcomes, such as tricking the internal logic
of SQL or displaying files by using code that invokes tables on the webservers. In some instances, an attacker is able to output contents into a file or inject commands alongside the SQLI, that get executed beyond the SQL query.

Towards the end making the final preparations for the presentation on Canva, I didn’t end up finding an appropriate more complex example. But this ended up working well since when practicing
the timing of the presentation we were slightly over the 6 minute mark. So even if I was to include a more complex demo, it would have taken up too much time on the presentation. I managed to write up and practice my script
for the presentation and made the final changes for the presentation ready for tomorrow.
<figure>
<img src="/img/Canva.png" >
<figcaption>
*Making the final changes to Canva for the presentation*
</figcaption>
</figure>

## Thursday 6/02
We presented our **SQL Injection** slideshow and was still cut off but not as close as I expected and actually managed to show off my demo this time. I was quite pleased how it turned out but during
my section I started losing my thoughts thinking that I started repeating my points during my presentation. This in future I will need to address and have more practice on my presentation and
ensuring I follow my script and guidelines. 

The rest of the day was spent on OverTheWire Natas challenges which I already previously participated in but mostly focused on create write-ups. Dylan Tchan and myself create a collaboration document to share our write-ups for future reference.
<figure>
<img src="/img/Write-up-natas.png" >
<figcaption>
*Level 3-4 Natas Basic Write-up.*
</figcaption>
</figure>
## Issues
This week didn’t have any major issues apart from the difficulty finding an appropriate demo for the presentation. The only other major issue would be procrastination by either attempting more OverTheWire
or getting side tracked with my **Career Management for IT Professionals Summer (31016)** Assignment. I’m still improving on communication with my team members and better improving time management.

## Goals/ To-do list
- ~~Do reflections each day to save time rather than on a single day.~~
- Try to do more wargames and improve write ups.
- Improve time management techniques.
- Improve team management and communication.
- Improve and make changes to website (background / presentation)
- Learn more about Git and Hugo to better edit my site.
- Understand the process of procedures in web pen-testing.
