---
layout: default
title: AMD AM4 CPUs - Ryzen Memory Voltage bugs
nav_exclude: false
has_children: false
parent: Tech Issues and How to Solve them
# grand_parent: 
# has_toc: false
search_exclude: false
last_modified_date: 2024-12-10
---
# AMD AM4 CPUs - Ryzen Memory Voltage bugs
{: .no_toc }

{% include toc.md %}

## Background

This bug is quite common amongst users especially after the Ryzen 5000 X3D CPUs came out. The bug in question mainly deals with users crashing when the PC is at idle, not under load. This is mainly due to the updated BIOS's incorrectly sending too low voltages to the memory controller, causing it to make incorrect decisions and mishandles the memory, and therefore crashes the system.

{: .note }
Theoretically a BIOS update should fix it, but in case it does not, a simple slight overclock is capable of handling this issue. If issues still persist, you may have to go through overclocking guides for stability and implement the one that's best suited for your CPU.

Do note to take care when altering voltages to not change other values in the BIOS as adjusting the clocks and voltages of any component can cause system instability or irreversible damage if done incorrectly, especially if you decide to do your own thing and not follow the guidelines.

{: .warning }
> *If you decide to do your own thing and cause irreversible harm to the PC, we cannot be held liable for any damage incurred by user error.*

---
## Symptoms and Diagnosis

- User is running an AM4 CPU, specifically Ryzen 3000 or 5000 series.
	- Almost all CPU variants are thought to have this issue, including X3D, X, XT and G. 
- [Specified](https://spec-ify.com/) or event viewer reports multiple <u>memory controller</u> WHEA errors, or similar WHEA reports related to the CPU.
	- Memory controller WHEA errors are more common with this kind of bug.
- The PC crashes when idling, not under load.
	- Crashes include BSODs, WHEAs, or instant shutoff for no reason and the PC rebooting.

## Potential Solutions

First step is to update the BIOS fully and ensure that the new BIOS has addressed this issue. This is the safest and easiest way to potentially fix it. If the issue still persists, you need to manually change the voltage.

You will need to go into BIOS and tweak voltage settings. Again, <u>tweaking voltage values and clocks beyond what is listed below can cause irreversible damage, and we will not assist in fixing a broken system if user error is suspected.</u>

Do note that different motherboards will have different BIOS's and layout so it may take some time looking for the correct menu. Once the correct menu has been found, adjust the voltages accordingly:
- **CPU VCore** offset to `+50mV` or `+0.05V`
- **VCORE SOC** offset to `+50mV` or `+0.05V`

{: .note }
Note that for some BIOS's, such as Gigabyte's, you need to set the **CPU VCore** to Normal, and then set **Dynamic VCore** to the offset value. The same applies to **VCORE SOC**. This is the same as setting offsets.

## Other potential Solutions

Should in case the initial **CPU VCore** and **VCORE SOC** values does not help in fixing the issue, adjusting them to higher values of potentially `+70/80mV` or `+0.07/0.08V` could give better results.

You may also have to edit other values, including memory controller voltages directly. Tweaking these should help in stability:
- **CPU VDDP/VDDG CCD** - Memory controller voltage, typical operation for DDR4 is `0.9-0.95V`.
- **CPU VDD18** - To deal with infinity fabric. Set to `1.85V` if issues still persist. Raise this by `0.05V` increments to a maximum of `2V` if issues still occur with regards to stability.

Additionally, look into overclocking guides to see VCore voltage and VSOC. Sometimes some manufacturers set really low values even below the offsets, in which case you may manually have to change it. 

For AM4, set both to `1.125V`, this is the known working values for most AM4 CPUs.