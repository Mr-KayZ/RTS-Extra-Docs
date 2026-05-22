---
layout: default
title: Riot Vanguard - Extremely Intrusive Anti-Cheat Software
nav_exclude: false
has_children: false
parent: Blog and personal opinions
search_exclude: false
last_modified_date: 2026-05-22
---
# Riot Vanguard - Extremely Intrusive Anti-Cheat Software
{% include toc.md %}
{: .no_toc }

## Riot Vanguard - An introduction
On April 7th, 2020, Riot Games announced the release of their new anti-cheat software, Riot Vanguard. This software does what any other anti-cheat does: detects cheats and hacks that's being used in their games, and take actions on cheaters and hackers accordingly. 2 months later on June 2nd, 2020, Valorant was announced which featured Riot Vanguard as the primary anti-cheat.

## What is an Anti-Cheat?
Before we dive into my critique of Riot Vanguard, I think its important to discuss what anti-cheats are and why they are becoming more invasive.

An anti-cheat is a software system that a game or developer utilizes to detect and block cheating in an online game. It scans for unfair programs like aimbots (which allow a user to "snap-on" to targets making aiming trivial), wall-hacks (which allows a user to see through cover or walls giving them an unfair advantage as they can tell where an enemy can be), speed-hacks (allows a user to move faster in games) and other cheats. For programs that don't have anti-cheat or trivial anti-cheats that can be bypassed, cheaters and hackers have a field day and can easily ruin the experience for everyone else who plays the game.

In the modern day, more and more anti-cheats are coming out being far more intrusive than previous generations, in order to combat more elaborate cheating methodologies and techniques. As a result, most if not all modern anti-cheats that provide significant protection against cheaters are kernel level anti-cheats (KAC for short). To explain what I mean by kernel level, this is where we have to talk about "privilege levels" for a PC operating system.

### Privilege Levels for an operating system
For any computer, be it phones, laptops or desktops, there are privilege levels which enforce access restrictions. The main reason they exist is to protect a system from bugs and malicious software by strictly limiting what different parts of a program can do and what access to what kinds of software and hardware a program has. 

These privilege levels are also referred to as Rings for x86 architecture from levels 0-3, with Ring 0 being the highest privilege level.
- **Ring 0 - Kernel mode**: This is the most privileged level, where the core operating system (aka the kernel) and essential device drivers run (like basic mouse and keyboard inputs for example). This zone has the highest access to all memory and hardware components, such as CPUs, and disk controllers.
- **Ring 3 - User mode**: This is the least privileged level, which most normal applications run at, such as web browsers and text editors. Ring 3 code cannot directly interact with the hardware (they are abstracted away) or access memory belonging to other processes here.

{: .info }
> **Rings 1 and 2**
>
> Rings 1 and 2 were historically meant for OS services and device drivers, but in modern operating systems most have split into either Ring 0 or Ring 3 as these intermediate levels don't really provide meaningful security or performance benefits over the simpler Ring 0 and Ring 3 model.
> 
> There is more nuance here, such as segment based protection levels offered by Rings 1 and 2 compared to page-table-based protections which modern OS's use, etc. but this is straying from the original topic. 
> 
> TL;DR - Modern Linux and Windows OSs use Rings 0 and 3 primarily for most software.

{: .info }
> **Exception Levels (EL) in non-x86 architecture**
>
> In non-x86 architecture such as ARM processors used in mobile devices and Apple laptops, the same concept also exist but are referred to as Exception Levels instead of rings, ranging from EL0 (User) to EL2 (Hypervisor) and EL3 (Secure Monitor).

#### *Why require higher privilege levels?*
When it comes to cheating software, cheaters have been extremely creative in their attempts to bypass current anti-cheat technology. 

There are many discussions on why KAC is now basically mandatory for any modern online game that aims to combat cheaters (one of my favorite ones is this one from [Adrian's Security Research](https://s4dbrd.github.io/posts/how-kernel-anti-cheats-work/) which goes into deep detail discussing how KAC came to and how they exactly work), but the general gist is that cheaters have been using more and more privileged access to software to bypass anti-cheat software, and the only way to stop them is bringing said anti-cheat software to higher and higher privilege levels so the cheating software and whatnot can be blocked/detected and malicious actors dealt with accordingly.

This basically means anti-cheats are now running at the highest levels of privilege at the moment, meaning they have direct access to all software and hardware and all memory a PC has on runtime.

**This is the status quo, and no, KAC isn't going away, no matter how much you hate it.**

If anything, thanks to more modern cheating techniques such as DMA and external dedicated cheating hardware, its predicted that anti-cheats may have to become more invasive and go even beyond the kernel - right into hardware.

### How modern cheats bypass current KAC technology
Modern cheaters use a mix of software, hardware and protocol-level tricks to bypass anti-cheats, including kernel-level anti-cheats. There are many methods, and I think its important to cover some of the common ones.

- **DMA (Direct Memory Access) cheating**: DMA means letting an external hardware read or write to a PC's main memory without going through the CPU or OS. This is one of the more "hard-mode" methods of cheating, and most well known in the cheating community.
    - A DMA card (often a PCIe or M.2 board) plugs into the host machine and can directly communicate with the RAM. Their initial purpose was for digital forensics, but cheaters have found a way to utilize this to bypass anti-cheat software.
    - These cards can forward the memory data to a second computer which runs the cheat software, allowing values such as offsets, coordinates, and whatnot from a game and then fed back as aim-assist, wall-hacks, etc.
    - Because the hack never touches a game's process or kernel in the first place in the host machine, 

## Riot Vanguard's 