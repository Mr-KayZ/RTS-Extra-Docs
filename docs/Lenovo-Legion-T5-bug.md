---
layout: default
title: Lenovo Legion T5 bug
nav_enabled: true
nav_exclude: false
has_children: false
parent: docs
search_exclude: false
last_modified_date: 2024-10-12
---
# Lenovo Legion T5 prebuilt - DPC_WATCHDOG_VIOLATION issues
## Background

The Lenovo Legion T5 has been experiencing issues related to its Nvidia GPU drivers. Users have reported frequent crashes, freezing, and blue screen errors (BSOD) when using certain Nvidia drivers, particularly `DPC_WATCHDOG_VIOLATION` BSODs.

The root cause of the GPU issues in the Lenovo Legion T5 appears to be an incompatibility between the Nvidia audio and graphics drivers and the other system components. This incompatibility can lead to conflicts that result in frequent crashes, freezing, and BSOD errors. **This is a manufacturing issue from Lenovo.**

Additionally, some users have reported that the PCI Express Root Port is also a contributing factor. This component, related to the video card, can cause hardware errors that further exacerbate the instability issues.

To address this issue, Lenovo has released a tool to address the current issue, details of which can be found here: [System may blue screen (BSOD) after installing Nvidia Graphics driver version 27.21.14.6231 - Legion T5-28IMB05 - Lenovo Support US](https://support.lenovo.com/us/en/solutions/ht513793-system-may-blue-screen-bsod-after-installing-nvidia-graphics-driver-version-2721146231-legion-t5-28imb05)

---

## Symptoms and Diagnosis

- Frequent crashes of programs.
- Black screens, freezes, GPU driver timeouts.
- BSODs with DPC_WATCHDOG_VIOLATION, or other BSODs blaming the NVidia drivers.

All symptoms are common to a misbehaving GPU driver. Only difference here is that issues will still persist even after a GPU driver reinstall via DDU.

## Known Solution

- First, follow the steps to [reinstall NVidia drivers via DDU](https://rtech.support/docs/factoids/ddu.html)
- Next run the [Lenovo patch tool](https://support.lenovo.com/us/en/solutions/ht513793-system-may-blue-screen-bsod-after-installing-nvidia-graphics-driver-version-2721146231-legion-t5-28imb05) after reinstalling the NVidia drivers.

This is in accordance with Lenovo guidelines and documentation, and has been proven to work across multiple systems.