---
layout: default
title: How to Troubleshoot - Steps and Practices for a beginner
nav_exclude: false
has_children: false
parent: Learning and Notes
search_exclude: false
last_modified_date: 2024-12-10
---
# How to Troubleshoot
{: .no_toc }

{% include toc.md %}

## Troubleshooting basics - The right mindset
A once famous Doctor Cox said most brilliantly in a show: 

{: .quote }
"Whatever sticks, that's the right dosage" 

This line came from Scrubs S01E01 - Possibly one of my most favorite TV shows out there (a must watch if you are looking for a new show to binge). The same idea applies to troubleshooting as well. 

The whole aspect of troubleshooting is to try a potential fix, and see if it works, and if not then try something else. The fix can be quick and simple, or it can be long and elaborate. Some are sure-fire fixes, others would reveal the true nature of the problem, or potentially make the problem worse (although if you stick to sound troubleshooting methodologies, this should not happen to you).

As an example, when someone comes to you and says they have a temperature problem with their PC, think about what are the primary reasons a PC can be hot. Gaming laptops by design will run hot regardless due to their powerful hardware crammed in tight boxes with limited outputs to dump the heat. Other reasons could be potentially the CPU thermal paste or GPU thermal paste getting dried up, causing them to overheat. Maybe it could be a bad airflow design in a case? Numerous items and possibilities out there.

A key thing to note is to keep an open mind about everything. One issue regarding a PC can be caused by numerous things. For example, say a PC is suddenly shutting down without you knowing why. You just boot into Windows, and within 2 minutes the PC just shuts down without any warning. This can be caused by a number of things, from:
- CPU overheating
- PSU being faulty
- Motherboard shorting out and shutting down
- Software issues, windows being messy, kernel driver issue, etc.

The only way to be sure is to test individual components and get a proper comprehensive view on what the PC is doing and thinking and what can cause the PC to freak out and act in that manner. Don't just assume something is the cause before you thoroughly go through every aspect about that particular potential cause before moving onto the next.

But how will you begin to know how to identify and fix them? Short answer: Google's your best friend.

## First and best tool: Google
It goes without saying your entry to troubleshooting stuff would begin with Googling. Google EVERYTHING you don't know about, and Google still even if you did know about them. 

It never hurts to learn more, and its better to take your time learning more about something before giving the fix than to immediately assume something else and state that's what the problem is. Keep an open mind, and don't jump to conclusions. Another famous quote applies here :

{: .quote }
"It is dangerous to assume because you might make an “ass” out of “u” and “me”.

The last thing you want is to give advice that causes issues to the user you are trying to help, such as replacing a CPU or Motherboard to fix a issue when in reality the issue was with the PSU all along. Sure the user could have done a warranty so financially it won't affect them, but the headache and mental stress incurred by a warranty replacement is not something anyone should go through for every single minor problem. (Ok PSU being faulty is a problem but you know what I mean!)

{: .important }
**Take your time and slowly get to the answer. Don't rush to help someone, analyze everything possible and take into account as much things as possible before coming to a conclusion.**

### Good sources and bad sources for information
Naturally, there are multiple sources of information. Some are reliable, while others, well, not so much. Some are outright scams, trying to get you to download their snake oil products, if not worse. This raises the question: How can I tell if my source is trustworthy? 

In other words, what makes a source reliable, and how can I trust it?

{: .warning }
> **Do not troubleshoot with AI "search engines"**
> 
> ChatGPT 4, Microsoft Copilot, Google Gemini, or any other AI tool should not be counted on for any form of support when troubleshooting anything at all. Google Gemini is now integrated into Google search, but you must not rely on just Gemini for answers. Select the sources directly and read properly so you can see if the sources are indeed what you are looking for.
> 
> These AI models are LLMs - Large Language Models with a search engine built into them. Effectively they are designed to read what you have typed and do their own similar searches accordingly, and then summarize the answer. Sometimes its good, but sometimes "AI hallucinate" and make up stuff on the spot. It is best to recheck what sources these AI are getting their answers from (if any) and see if they really do contain the information you need. (This is why your teachers told you Wikipedia is not a source!)
> 
> Ask yourself this, would you let an AI diagnose your medical condition, or would you go to a doctor instead who can give proper advice and diagnosis? (Recall why people think WebMD as a joke, being a "medical search engine".)

With the AI warning out of the way, we can go into the main portion of answering this question.

#### <u>Manufacturer statements</u>
First and foremost the best source will be from the manufacturers themselves. If there's a massive issue with regards to a product line failure, for example, then the manufacturer will come out with a statement regarding the failure and (normally) address them. One of the more famous examples would be [Intel's absolutely disastrous 13th and 14th gen instability issues](https://www.tomshardware.com/pc-components/cpus/intel-issues-official-statement-on-core-k-series-crashes-stick-to-intels-official-power-profiles) as reported by numerous news sites and tech forums. (FYI Toms Hardware is a really good source for a lot of information).

#### <u>Forums</u>
Another excellent resource is forums. These platforms are where individuals with various issues and experiences share their problems, offer solutions, and discuss fixes. Some reliable options include Reddit, XDA Developers, and Tom's Hardware. By reading through multiple posts, you can see how different people tackle an issue and whether anyone has found a solution. For example:
![/RTS-Extra-Docs/assets/img/How-to-troubleshoot/Forum_posts.png](/RTS-Extra-Docs/assets/img/How-to-troubleshoot/Forum_posts.png)

Forums are also valuable for reviews because they provide real user experiences, diverse opinions, and detailed discussions. They foster a sense of community where users support each other and offer up-to-date information, making them a reliable resource for comprehensive and authentic reviews.

Sometimes these forums will have a news section attached to them, which also contain plenty of solid information to read through and get information from. [Tom's Hardware](https://www.tomshardware.com/) is one such example where they provide detailed coverage and information with regards to a tech issue.

{: .note }
> **Personal opinion:** One of the great things about tech news is that it's mostly science-based and evidence-driven. There aren't many untrustworthy sources because, at the end of the day, these news pieces offer quantitative information rather than qualitative. 
> 
> This means the information is based on numbers, which can't easily be reworded or taken out of context like other types of information. When someone does try to manipulate the numbers, people will definitely call them out on it, and rightfully so. This is also why forums are excellent for covering tech news articles too.

#### <u>YouTube</u>
YouTubers who are well known in their space are often are also great sources of information themselves. Signs of a good youtuber would be one who list their own sources of information and what they are basing their information on (experimentation, personal reviews, etc.) - Forum reviews of youtubers are also great to tell if a youtuber is good or not (and despite it all, also heavily opinionated). The following youtubers, in my opinion, are solid options when it comes to reviews, analysis, and how to troubleshoot:
- [GamersNexus](https://www.youtube.com/@GamersNexus) (General tech journalism)
- [Level1Techs](https://www.youtube.com/@Level1Techs) (Analysis, Design talk, etc.)
- [Salem Techsperts](https://www.youtube.com/@SalemTechsperts) (Tech shop blogging, general advice, good practices for troubleshooting, etc.)
- [Dawid Does Tech Stuff](https://www.youtube.com/@DawidDoesTechStuff) (Reviews, Tech blogging)

This small list are a group of youtubers I watch regularly to get better informed about the industry, learn about good practices on troubleshooting, learn about current massive issues and what is needed to fix them, etc. All of them offer good sources of information with good sources and evidence to support them too.

{: .note }
> You may notice that **Linus Tech Tips** (Otherwise referred to as **LTT**) is not present in this group despite being one of the bigger "tech YouTubers" out there. While it is true that the **Linus Media Group** (**LMG**) does cover information that is tech oriented, it is important to take into account that they are a media group that is on the record for producing statements that are misleading at best and factually incorrect at worst. They should be treated as a entertainment channel, not for following actual tech advice.
> 
> I am not saying its a bad idea to watch LTT, they are fun to watch, and I watch them regularly too, but for general entertainment, not learning. I am just stating its best to rely on other sources as well when trying to take advice from them directly, and not just trusting them blindly as a single source.
> 
> The same is true for any YouTuber actually. Don't just blindly trust everything everyone is saying without proper sources backing them up.

{: .important }
**When relying on a youtuber for a source, always refer to their sources and check other people's opinions and data on the matter as well. A single source is not good enough, especially if said youtuber may have taken information out of context.**
### The bad sources
Naturally we will have to cover this section too. Generally saying, a bad source of information or review are any that are trying to sell you a product. While sometimes the fixes and troubleshooting steps provided in them sometimes are good, most of the time these are actually copy pasted from other reputable forums and statements from more reputable sources, and are utilized as a front to get you to "Download their product" which apparently can solve every problem under the sun - this is clickbait and false advertisement.

Another sure giveaway is the sheer number of ads and "Sales" these websites will entail to make you think you will get a brilliant deal on a product that you will never need to use once, are either snake oil, or will actually do harm to your computer instead.

{: .important }
> A classic example of this would be the MiniTool "troubleshooting posts" for a issue, which sometimes give very generic answers to solving a problem "How to Fix DISM Error 0x800f081f on Windows 10?"
> 
> Almost all of these articles will state the general "Download our tool to fix all your issues!" while giving a very generic statement about what the issue is without delving into more information regarding it and what can be the root cause for them, and then proceed to give generic fixes about those issues. This is plain false advertisement and clickbait.
> ![/RTS-Extra-Docs/assets/img/How-to-troubleshoot/minotool.png](/RTS-Extra-Docs/assets/img/How-to-troubleshoot/minitool.png)
> MiniTool is a partitioning tool (Which we do not support as its paid and closed source) that is a paid for service to do multiple things. While not a bad tool by itself, we disavow it due to its incessant advertisement and false marketing. Any company that partakes in these practices automatically are subject to the same treatment as "bad source".

That being said, it isn't a bad idea to try the other generic fixes provided by them anyways. If you can ignore the sheer number of advertisements and their constant selling of their unnecessary software, you can try out the general fixes offered by them, and see if they aid in the situation. More often than not, the suggestions are generally fine and nothing harmful per say.

{: .note }
> This is not inherently true for certain other guides and advertisements. Some "guides" online can be scams and might try to get you to install malware in promise of fake "performance gains" or the likes. Remember that the internet can be a dangerous place, and taking steps to ensure you practice safe browsing should always be considered.
> 
> TL;DR - Do not go searching up random stuff and end up in shady websites to download random programs - That is a surefire way to get yourself infected with a virus or worse.

## Asking the right questions
To troubleshoot, one must get all the information necessary to proceed. This means asking questions about everything - how long they had the issue for, what the hardware is like, hardware specifications (even manufacturer numbers might come into effect here depending on the issue), warranty status on the product, is it a prebuilt or not, etc.

With all these questions, you build a mental picture of the issue at hand, as well as the user's capability to answer such requests for information appropriately.
#### <u>Gauging the troubleshooting skill of the user</u>
Remember that not everyone you speak to might be well versed in electronics and hardware as you might be. You can go on about motherboard VSOC voltages, and the end user would be completely confused as they might not even understand what a motherboard is. For remote based tech support, this rings even more true for certain situations.

One of the few questions I might ask with regards to user skill level are the following, this helps me gauge possible user skill level with regards to tech based stuff so I know how I should discuss certain topics with regards to the user so they can understand what to do (since I do remote helpdesk):
- "*Is the product you are using a prebuilt - or is this a custom build?*" - This helps me know if the user built the desktop by themselves or not. Generally speaking, users who built a computer by themselves generally know a bit more about hardware in general and therefore can follow more complex instructions (i.e. require less handholding).
- "*What are the troubleshooting steps you have taken and go into as much detail as possible regarding this issue.*" - If the user goes into deep lengths and analysis with regards to the issue, for example listed error codes and their meaning, that means the user knows very well what they are talking about and are extremely knowledgeable about computer hardware and software. If they state something generic as "I shut down the computer, that's it", it may be safe to assume the user lacks troubleshooting know-how and requires more explanation with regards to each troubleshooting step you may request them to do.

#### <u>Figuring out the issue - How my mindset works</u>
Ask as many questions related to the issue as you can so you can identify what the issue is and try to implement the appropriate fix accordingly. Don't worry if a fix did not work, that just means your diagnosis was wrong and you can try another fix instead. Sometimes revisiting the older information again to see what is wrong can aid you tremendously here too - allowing yourself to see the broader picture and hidden details you may have missed due to hyper fixating on one particular detail of the issue at hand.

How I approach issues is with a classification system, with sub-classification of issues depending on the information I can get out of the user. My classification of issues goes something like this:

- Try to identify if this is a hardware or software issue.
	- If Software, try to identify what kind of software issue it is, driver or kernel or whatnot.
		- Try to then search if there's any potential fix for this issue. For drivers you try to reinstall the drivers from the motherboard's page or product manufacturer's website. If kernel issue, try to run DISM/SFC and hope that works, or perhaps attempt a in-place upgrade/reinstall to see if that might aid the user.
			- Note that these are very generic fixes and depending on the issue, you may have more steps/subclassifications to further identify what the issue is and apply the appropriate fix.
	- If hardware, try to identify what faulting hardware is causing the problem, whether that is by analyzing WHEA reports, or of a certain piece of the PC is non functional, such as no display to the monitor (which you can use this awesome guide to try and fix it [here](https://rtech.support/guides/no-image-troubleshooting/).)
		- Normally hardware failure cannot be fixed easily, unless its some form of firmware bug that is causing the mess - Try and attempt a firmware update if possible. (**Warning:** If anything occurs during the firmware update of anything, such as keyboard, motherboard or controller, etc, such as it losing power or shutting down, that device may be permanently bricked and you will have to replace the unit unless a re-flash option is available.) 
		  
		  Otherwise, replacement of that hardware is the only fix here usually. If there's warranty present on the device, pursuing warranty via [RMA request](https://en.wikipedia.org/wiki/Return_merchandise_authorization) might be the go-to here.
			- Again, these are very generic fixes and depending on the issue, you may have more steps/subclassifications to further identify what the issue is and apply the appropriate fix.

## Learning more about issues and computers
The more help cases you go through, and the more you observe, the more patterns you begin to see with regards to issues, and see how each issue seem to manifest itself. Its very useful if you start by researching common tech issues, going through solved cases on Reddit, StackOverflow, Microsoft forums, etc., and seeing how issues are presented and how to diagnose them - The more you research the better.

One excellent resource out there are general IT glossaries that explain many different concepts and ideas extremely well. Simply searching up IT glossary in Google will yield multiple solid results. 

I primarily utilize [Lenovo's glossary](https://www.lenovo.com/ca/en/glossary/) to explain concepts to me (ignore the constant ads if you can) and go through a lot of detail and information that even a beginner can understand. Do note that their wording can be a bit skewed with regards to how they constantly try to upsell stuff such as "Why NVidia DLSS is very important in gaming, and why you should have it too!", but apart from that the information on it is accurate and solid.
### The Hardware
It also helps if you understand computer hardware and software as well, particularly how operating systems work, and how CPU interacts with RAM, GPU, etc. I personally would recommend learning about the hardware first, before moving onto software, as the software portion, especially operating systems, build upon hardware knowledge.

One of the better starting points for hardware would be learning about the main components on what makes a computer hardware wise, [this website from Carnegie Cyber Academy](http://www.carnegiecyberacademy.com/facultyPages/computer/computers.html) explains computer hardware in a very easy to understand graphics and depiction. Although the information on it is a bit dated, they will still hold true in the modern day, and you can build off from there. 

What I would do later is search up these individual components and see how those components work, such as "How does a CPU work" after learning the general importance of a computer, and from there, "How does an ALU work", or "How does cache work", "What's the difference between L1, L2, and L3 cache", etc. - By learning about these individual components within individual components, you can get a better understanding of how a computer works in general, grounding your knowledge even more.

Remember, don't hesitate to search anything you do not understand. Google is always the first and best tool out there after all.
### The Firmware
The firmware of any hardware can be described as the "software to run the hardware". All modern electronic components, be it mice, keyboards, motherboards, etc. contain microchips that can do so many different functions, from displaying RGB based on the user's taste, to accept button inputs to change the functionality of the device (such as changing the DPI speed of the mouse), and so much more.

All of these microchips contain code within them that allows users to run these customization tools and whatnot on these devices, which is referred to as firmware. Firmware programming is a complex thing by itself, and often requires knowledge of the circuitry of the device in question too to make sense of how the firmware even works. More often than not, it can get really complex really quickly.

For most end users, firmware fixes are something made by developers, which only the end user needs to apply. If there's a firmware update, most of the driver applications for these hardware products have firmware update software which enables you to update the firmware of these device. Sometimes these firmware can be buggy, which would require a downgrade of the firmware instead.
### The Operating System
After learning a bit about the hardware and general components, its time to tackle the more complicated stuff: The software. More specifically, the operating system as a whole, and how an OS functions. This is very far more complex than the average software, but allows you to see beyond normal software and understand deeper computer issues as well once you understand how an operating system works.

An operating system (OS) is like the manager of a computer. Its the main software that manages a computer's hardware and software resources, providing common services for a computers programs, such as scheduling tasks, executing applications and controlling peripherals (through drivers and whatnot) - Essentially, it acts as an intermediary between the user and the computer hardware, ensuring everything runs smoothly and efficiently.

There are many aspects that go into making an operating system, and way too much to properly describe it here. But one of the best resources for understanding an operating system once you know more about hardware is to look at [Philipp Oppermann's Writing an OS in Rust](https://os.phil-opp.com/) blog, which goes through the full detail on what makes an operating system an operating system.

While he utilizes Rust as the example programming language of choice, an operating system can be made using any language necessary, and you do not need to know programming at all to understand what is going on - all that matters is the contextual guidance.

