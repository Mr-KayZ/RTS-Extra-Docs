---
layout: default
title: WHEA-Analysis - 03 - AMI Nonsensical WHEA error
nav_exclude: false
has_children: false
parent: Learning and Notes
# grand_parent:
# has_toc: false
search_exclude: false
last_modified_date: 2025-11-20
---
# AMI nonsensical WHEA error
{: .no_toc }

{% include toc.md %}

## Who is AMI?
AMI, or American Megatrends, Inc., is an international hardware and software company that specializes in PC hardware and firmware mainly. Most people would usually know them from seeing a screen like this when they [reset their CMOS](https://rtech.support/factoids/cmos/) of their motherboard (or reset their BIOS to default):

![/RTS-Extra-Docs/assets/img/AMI_WHEA/BIOS_Reset.jpeg](/RTS-Extra-Docs/assets/img/AMI_WHEA/BIOS_Reset.jpeg)

This may seem confusing for some, as many would have purchased a brand motherboard, such as ASUS, or MSI, or Gigabyte. Or it could be a prebuilt from Dell or HP, but nowhere does it state anything about AMI anywhere, and some may even confuse this as their PC having a virus of some kind. Seeing this sort of screen is no reason to panic, and in fact is completely expected upon a CMOS reset.

{: .info }
> If you wish to know what BIOS/UEFI is, it is recommended you refer to the [BIOS update guide](https://rtech.support/guides/bios-update/#what-is-bios-how-do-i-update-it) in the r/techsupport wiki to find more information on what BIOS and UEFI are and why it is extremely important for any motherboard to function.

The BIOS/UEFI firmware you see in most modern computers is in fact often manufactured by independent firmware vendors (IFVs). Motherboard manufacturers like Gigabyte and ASUS produce the hardware, but the firmware the motherboard utilizes in order to interact with modern Operating Systems such as Windows and Linux is typically sourced from IFVs. 

The largest and most common firmware vendors are American Megatrends (AMI), which produces AMIBIOS (for legacy BIOS) and Aptio (UEFI firmware). These motherboard manufacturers then modify and customize the firmware from AMI with their own branding and specialized GUI (if UEFI) for their specific motherboards.

While AMI remains as the largest vendor for BIOS/UEFI, there are other corporations that also produce firmware for motherboards as well:
- **Phoenix Technologies**: Another major vendor like AMI
- **Insyde Software**: Produces `InsydeH2O` UEFI firmware, commonly found in laptops, notebooks, servers, IoT devices and embedded systems.
- **Nanjing Byosoft Co., Ltd** (also known as **Byosoft**): A BIOS vendor authorized by Intel, primarily serving enterprise and infrastructure markets.
- **SeaBIOS**: An open-source BIOS implementation used as a payload in open-source projects like `coreboot`, and also utilized as the default firmware in virtualization platforms like QEMU and KVM for virtual machines.

## Specify has a warning WHEA error
This section assumes that you use Specify and have come across a WHEA error with severity "Information" (not "Warning"). However, the device is unable to be identified, and you simply see the following GUID:
- `93A41C2F-A09F-E7C2-AC1F-F2488F03EEC3` - Yes. It is always this EXACT GUID every single time.

{: .info }
> Specify is a snapshot viewer, as in it collects data from the system it's running on and then passes all this data to a website, [spec-ify.com](https://spec-ify.com/), which presents data in a structured way allowing users to view the status of their machines, or aid tech support agents in analyzing systems and figuring out what's wrong with them or general checkup.

This means absolutely nothing to everyone so far as the documentation is all under wraps. What we are able to glean from countless hours of research (Thank you [JimmahDean](https://github.com/JimmahDean) for doing the deep dive into this and teaching me all I know about this) and disappointing curt non-answers from manufacturers, it's somehow related to the ACPI PHAT (Platform Health Assessment Table). Unfortunately while the WHEA record does in fact contain structures and more information going into great detail with detailed error packets, the specific meaning of this GUID and its associated data are not publicly documented in standard ACPI specifications.

### ACPI shenanigans
ACPI stands for Advanced Configuration and Power Interface. It is an open industry standard specification that provides an interface for Operating System-directed configuration and Power Management (OSPM). ACPI enables the operating system to discover, configure, manage, and control hardware devices and power management through firmware interfaces, rather than requiring platform-specific BIOS implementations. The PHAT table, specifically, is a mechanism where platform firmware can expose health-related telemetry that may be useful for software running within an operating system - typically encompassing things not otherwise enumerable during OS runtime, such as versions of pre-OS components and firmware health status.

### The unknown GUID
The GUID `93A41C2F-A09F-E7C2-AC1F-F2488F03EEC3` appears in WHEA records as a Section Type identifier. According to research, this appears to represent a vendor-specific or platform-specific health assessment record. The ACPI specification defines PHAT Record Types 0x0002-0x0FFF as "Reserved for ACPI specification usage," while 0x1000-0x3FFF are reserved for platform vendor, hardware vendor, and firmware vendor usage respectively. This particular GUID may fall into one of these reserved categories, particularly those designated for AMI (American Megatrends Inc.) BIOS implementations.

The pattern of seeing `VenHw(93a41c2f-a09f-e7c2-ac1f-f2488f03eec3)` in error packets suggests this is formatted as a UEFI device path using the Vendor Hardware Device Path node type. The "VenHw" prefix indicates a vendor-specific hardware device path node that is not defined by standard UEFI specifications, commonly used for platform-specific implementations like memory-mapped controllers or proprietary firmware interfaces.

### Wait that's it?
And that's all we know. All further information regarding the specific purpose, trigger conditions, and diagnostic meaning of this particular WHEA information record and GUID are internal to AMI and platform vendors, with no public documentation available to offer a reason or cause for this particular WHEA informational message appearing in the Specify report.

From observations of all manners of motherboards running Specify, we have noticed the following chipsets are the only one to produce this GUID:
- Z690 and Z790 (Specifically Intel based platforms. No AMD platforms have yet tossed this type of error so far).
- Doesn't matter what brand it is (MSI, ASUS, Gigabyte, Dell, etc.) - If it utilizes an AMI BIOS, it can have this error.

{: .note }
> As of the time of writing this, r/techsupport helpers (including I) have internally classified this as the "AMI-Nonsensical WHEA error". Until AMI or Microsoft actually provides a proper description as to what could the GUID actually mean or point to, this WHEA error will be disregarded when troubleshooting user issues.

## Credits:
- Thank you once again [JimmahDean](https://github.com/JimmahDean) for everything he has done so far to help me get a avid interest into hardware and tech as a whole, especially informing me about this particular weird case of WHEA reports.
- The following thread: [https://www.bleepingcomputer.com/forums/t/795915/how-can-i-speak-with-someone-knowledgeable-on-complicated-topics/](https://www.bleepingcomputer.com/forums/t/795915/how-can-i-speak-with-someone-knowledgeable-on-complicated-topics/)