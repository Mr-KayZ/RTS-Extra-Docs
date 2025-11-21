---
layout: default
title: Firmware Bugs in NVMe SSDs with HMB
nav_exclude: false
has_children: false
parent: Tech Issues and How to Solve them
# grand_parent: 
# has_toc: false
search_exclude: false
last_modified_date: 2025-02-27
---
# Firmware Bugs in NVMe SSDs with HMB - Memory leaks
{: .no_toc }

{% include toc.md %}

## Background
Symptoms of users can be varied, but allegedly the issue is freezes when a system is under load and is doing lots of paging, like running a game. System freezes occur, no BSODs. Others report game crashing due to "Out of memory" error, etc.

These primarly seem to occur if the NVMe is DRAM-less and utilizes HMB instead to achieve better performance, allowing cheaper NVMes to be produced as they do not require a dedicated DRAM cache.

### What is HMB?
Host Memory Buffer (HMB) is a technology used in SSDs to reduce costs by eliminating the need for onboard DRAM. Instead, HMB utilizes the system's DRAM (AKA the normal RAM) as a cache for the SSD. This approach allows SSDs to maintain good performance without the added expense of dedicated DRAM.

In traditional SSDs with DRAM, the DRAM stores a mapping table that tracks the locations of data on the SSD, leading to faster access times. However, DRAM-less SSDs with HMB use a portion of the system's DRAM to perform this function, which can still provide decent performance but may not be as fast as SSDs with dedicated DRAM.

HMB is particularly beneficial for cost-sensitive applications, as it helps lower the price of SSDs while still delivering acceptable performance for everyday tasks.

More information can be found [here](https://www.pcworld.com/article/784380/host-memory-buffer-hmb-the-dram-less-nvme-technology-thats-making-ssds-cheaper.html).

### Main issue
The HMB driver operates as usual, but the SSD firmware can have bugs. This can cause a dangerous loop where the system attempts to cache data from the DRAM of system memory (as it would in a typical SSD with DRAM), fails, and reverts to storing the data in the system memory, which is already allocated.

This cycle continues, resulting in a memory leak. To be clear, this is not a fault of Windows, the HMB driver is working as intended. This is a fault of the SSD firmware failing to cache the items from DRAM.

{: .note }
> Fun fact, this was what was causing the crashes in the original Western Digital drives for Windows 24H2, until WD addressed this by issuing an emergency update for the firmware of the SSD.

---
## Symptoms and Diagnosis
- User is running a DRAM-less drive that utilizes HMB.
    - Does not need to be the C drive, any drive will do, especially if the game is stored on said drive.
- User experiences crashes or freezes when theres lots of load to and from a drive. 
   - This most commonly will occur in games since they require massive reads and writes usually.
- The crashes are somewhat inconsistent usually, and hard to identify. But when dumps are present user may find storeport calls present in the stack dump, possibly even HMB calls.
   - The sporadic nature of these crashes make them hard to identify.
- The firmware of the SSD is outdated, users mentioning similar crashes with same SSD.
   - Forum posts will be a good start to hunt down these issues.

## Potential Solutions
The main fix is to look for a firmware update for the SSD by downloading the accompanying software for the SSD. This is the best recommended method for this issue.

Alternatively if a firmware update is not present, and you have confirmed that the HMB driver messing up with the faulty NVMe firmware to be the cause of the crashes (by reconfirming with forum posts), you may proceed to disable HMB directly by a registry edit.

{: .important }
> *Doing this will result in DRAM-less drives in your system to operate at slower speeds, causing performance loss, so update the firmware once available to regain normal speeds with HMB enabled (i.e. delete the below registry key once you update firmware).*

### Method 1: Saving as a .reg file
1. Open up notepad.
2. Copy and paste the following into the note file:

   ```
   Windows Registry Editor Version 5.00

   [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\StorPort]
   "HmbAllocationPolicy"=qword:0000000000000000
   ```
3. Save this `.txt` file as a `.reg` file by simply renaming the extension. Preferably name it as `HMB_Disable_.reg`.
4. Run the `DWM_Fix.reg` file. You may have a UAC (User Account Control) dialogue popup.

Once that is done, reboot the computer to see the changes apply.

### Method 2: Using Regedit

{: .warning }
> *The registry is very powerful and allows you to change many things regarding how Windows operates, but it can be dangerous if you mess up adding keys or values to areas which do not belong. If you decide to do your own thing, you may end up with a broken Windows install which can only be fixed with a [reinstall of Windows](https://rtech.support/windows), unless you have backed the registry or have a System Restore point. Note that this also is no guarantee if you cannot access Windows to begin with if it is that broken.*

Open up registry, head to the following registry hive:
- `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\StorPort`

In this registry hive, add a new `QWORD(x64)` entry:
- Name: `HmbAllocationPolicy`
- Value: `0` (Default)

Once that is done, reboot the computer to see the changes apply.