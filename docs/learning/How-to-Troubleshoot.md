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

#### <u>The bad sources</u>
Naturally we will have to cover this section too. Generally saying, a bad source of information or review are any that are trying to sell you a product. While sometimes the fixes and troubleshooting steps provided in them sometimes are good, most of the time these are actually copy pasted from other reputable forums and statements from more reputable sources, and are utilized as a front to get you to "Download their product" which apparently can solve every problem under the sun.

Another sure giveaway is the sheer number of ads and "Sales" these websites will entail to make you think you will get a brilliant deal on a product that you will never need to use once, are either snake oil, or will actually do harm to your computer instead.

{: .important }
> A classic example of this would be the MiniTool "troubleshooting posts" for a issue, which sometimes give very generic answers to solving a problem "How to Fix DISM Error 0x800f081f on Windows 10?"
> 
> Almost all of these articles will state the general "Download our tool to fix all your issues!" while giving a very generic statement about what the issue is without delving into more information regarding it and what can be the root cause for them, and then proceed to give generic fixes about those issues. This is plain false advertisement and clickbait.
> ![/RTS-Extra-Docs/assets/img/How-to-troubleshoot/minotool.png](/RTS-Extra-Docs/assets/img/How-to-troubleshoot/minitool.png)
> MiniTool is a partitioning tool (Which we do not support as its paid and closed source) that is a paid for service to do multiple things. While not a bad tool by itself, we disavow it due to its incessant advertisement and false marketing. Any company that partakes in these practices automatically are subject to the same treatment as "bad source".

That being said, it isn't a bad idea to try the other generic fixes provided by them anyways. If you can ignore the sheer number of advertisements and their constant selling of their unnecessary software, you can try out the general fixes offered by them, and see if they aid in the situation. More often than not, the suggestions are generally fine and nothing harmful per say.