---
layout: default
title: WHEA Analysis
nav_exclude: false
has_children: false
parent: docs
search_exclude: false
last_modified_date: 2024-10-12
---
# SPECIFY - WHEA error records - CMCI_NOTIFY_TYPE_GUID

Suppose you encounter a WHEA in specify where there are no specific MCE records (Its a CMCI notify type - **Corrected Machine Check Interrupt**), this means you will have to go through the error packets and figure out what it means.

For context, CMCI - Corrected Machine Check Interrupt - Means that the WHEA error was encountered by Windows, but was corrected accordingly. This is why the severity of the crash is not fatal but "Warning".

![[Pasted image 20241210131704.png]]

## Error Descriptors

To do this, we analyze what the error packet specifically says. The specify report has multiple error descriptors split up into sections (in accordance with the error packets). Each section of the packet refers to a section in the Error Descriptors.
### Error Descriptor Sections
In this example, we have 4 sections A, B, C, D, corresponding to the 4 sections represented in the error packet:

![[Pasted image 20241210155923.png]]
One way to tell one section from another is that all sections start with offset `0x00`. This is true for all offsets present in the Error packet. Each error descriptor has their own details, mainly the section type. The section type depicts what GUID the error packet belongs to so it can be identified accordingly.

You can see in Sections `A`, `B` and `D` of this particular packet, the section types refer to the following generic calls that gives us more information about the WHEA:
- Section A - `MEMORY_ERROR_SECTION_GUID` - This tells us the WHEA is reportedly within the memory section of the device. In this case it is the CPU.
- Section B - `PROCESSOR_GENERIC_ERROR_SECTION_GUID` - This is what tells us the CPU is at fault. Still, we are not fully aware whether if by memory, it means the memory controller or cache.
- Section D - `RECOVERY_INFO_SECTION_GUID` - Contains the recovery info, since this was a corrected machine check, the details are present here on what steps Windows has taken to fix this.
### WHEA_XPF_MCA_SECTION
You may notice there is one section here which contains a "UNKNOWN GUID", section C. The GUID states `8a1e1d01-42f9-4557-9c33-565e5cc3f7e8`, which Googling reveals it is a [WHEA_XPF_MCA_SECTION](https://learn.microsoft.com/en-us/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_whea_xpf_mca_section). This is a machine check exception error section structure, meaning we can find more details regarding it. This is exactly what we need out of this 

The section structure is as follows:
```C++
typedef struct _WHEA_XPF_MCA_SECTION {
  ULONG             VersionNumber;
  WHEA_CPU_VENDOR   CpuVendor;
  LARGE_INTEGER     Timestamp;
  ULONG             ProcessorNumber;
  MCG_STATUS        GlobalStatus;
  ULONGLONG         InstructionPointer;
  ULONG             BankNumber;
  MCI_STATUS        Status;
  ULONGLONG         Address;
  ULONGLONG         Misc;
  ULONG             ExtendedRegisterCount;
  ULONG             ApicId;
  union {
    ULONGLONG                   ExtendedRegisters[WHEA_XPF_MCA_EXTREG_MAX_COUNT];
    WHEA_AMD_EXTENDED_REGISTERS AMDExtendedRegisters;
  };
  MCG_CAP           GlobalCapability;
  XPF_RECOVERY_INFO RecoveryInfo;
  ULONG             ExBankCount;
  ULONG             BankNumberEx[WHEA_XPF_MCA_EXBANK_COUNT];
  MCI_STATUS        StatusEx[WHEA_XPF_MCA_EXBANK_COUNT];
  ULONGLONG         AddressEx[WHEA_XPF_MCA_EXBANK_COUNT];
  ULONGLONG         MiscEx[WHEA_XPF_MCA_EXBANK_COUNT];
} WHEA_XPF_MCA_SECTION, *PWHEA_XPF_MCA_SECTION;
```

With this, we can now translate the error packet. Remember, all error packets start from offset 0x00 in Specify:
```
03 00 00 00 02 00 00 00 05 7e 33 ba 71 4a db 01  - 0x00 - .........~3ºqJÛ.
0b 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  - 0x10 - ................
00 00 00 00 00 00 00 00 35 01 01 01 00 40 20 9c  - 0x20 - ........5....@ .
08 19 b3 a4 06 00 00 00 00 00 00 00 fe 0f 1a d0  - 0x30 - ..³¤........þ..Ð
0a 00 00 00 0b 00 00 00 00 00 00 00 b0 00 10 00  - 0x40 - ............°...
01 24 1f 1a 6e 00 00 00 fd 01 00 00 27 00 00 00  - 0x50 - .$..n...ý...'...
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  - 0x60 - ................
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  - 0x70 - ................
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  - 0x80 - ................
3b 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  - 0x90 - ;...............
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  - 0xA0 - ................
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  - 0xB0 - ................
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  - 0xC0 - ................
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  - 0xD0 - ................
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  - 0xE0 - ................
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  - 0xF0 - ................
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  - 0x100 - ................
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  - 0x110 - ................
```

This looks a bit hard to read, so let's pretty it up a bit by splitting up bytes  into what we know so we can translate it properly. We would need to know the size of the items present, and the [variable types in the struct](https://docs.rs/windows-sys/latest/windows_sys/Wdk/System/SystemServices/struct.WHEA_XPF_MCA_SECTION.html) already tells us how many bytes each variable is already:

| Variable Name               | Variable Type   | Variable Size (Bytes) |
| :-------------------------- | :-------------- | --------------------: |
| Version Number              | ULONG           |                     4 |
| CPU Vendor                  | WHEA_CPU_VENDOR |                     4 |
| Timestamp                   | LARGE_INTEGER   |                     8 |
| Processor Number            | ULONG           |                     4 |
| Global Status               | MCG_STATUS      |                     8 |
| Instruction Pointer         | ULONGLONG       |                     8 |
| Bank Number                 | ULONG           |                     4 |
| MCI Status                  | MCI_STATUS      |                     8 |

These are the ones that we care for the most. As a matter of fact, almost everything after MCI status can be ignored as we do not have internal documentation regarding how those work. We can now split the error packet accordingly:

```
03 00 00 00             - Version No.
02 00 00 00             - CPU Vendor
05 7e 33 ba 71 4a db 01 - Timestamp
0b 00 00 00             - Processor No.
00 00 00 00 00 00 00 00 - MCG Status
00 00 00 00 00 00 00 00 - Instruction Pointer
00 00 00 00             - Bank Number
35 01 01 01 00 40 20 9c - MCI Status - This is the one we need!!!

We can ignore the rest here:
08 19 b3 a4 06 00 00 00 00 00 00 00 fe 0f 1a d0
0a 00 00 00 0b 00 00 00 00 00 00 00 b0 00 10 00
01 24 1f 1a 6e 00 00 00 fd 01 00 00 27 00 00 00
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
3b 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
```

Another thing to take note here is the fact that all of these values are little endian, so the bytes are "backwards". In this case, `03 00 00 00` is read `00 00 00 03`. `12 34 56 78` would be read `78 56 34 12`, etc.

We can now translate the MCI status codes into the following:
- CPU Vendor - AMD
- Processor Number - `11` (Thread 11, Core 5)
- MCI status - `01 35` - Memory Error - (After running `wheaceerror.py` - Thanks Jim)
![[Pasted image 20241210172654.png]]

Considering all other surrounding errors, this could be a memory controller level error too. But this is enough to tell us all the details for now.
