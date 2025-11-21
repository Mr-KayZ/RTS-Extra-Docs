---
layout: default
title: DWM stutter and lag on Chromium based Services
nav_exclude: false
has_children: false
parent: Tech Issues and How to Solve them
# grand_parent: 
# has_toc: false
search_exclude: false
last_modified_date: 2025-11-20
---
# DWM stutter and lag on Chromium based Services
{: .no_toc }

{% include toc.md %}

## Background
Symptoms of users mainly indicate issues with Electron or Chromium based services since the update to Windows 11 24H2 (at the time of writing, this bug still persists in 25H2). Services include applications such as Discord, Visual Studio Code, and even Chromium based browsers such as Edge or Chrome itself, particularly when the user alt-tabs from a GPU heavy process such as a video game or equivalent.

Users describe the issue as graphical glitches manifesting in the form of:
- Parts of the interface being updated (Such as scrolling through discord, but only a third of the window is being updated while the rest is frozen).
- Section of the interface around the mouse cursor only updating (a bit more rare usually).

Multiple fixes have been offered, ranging from DDU and reinstallation of GPU drivers to disabling Hardware Accelerated GPU Scheduling (HAGS) and everything in between have been offered, including full reinstalls of the OS. While these may seem to temporarily resolve the issue, the bug still persists and eventually reveals itself a few days to a few weeks after attempted fix has been applied. It also does not matter what GPU manufacturer a user may utilize: NVidia, AMD and Intel GPUs all face this bug - this would indicate to one with a keen eye that the issue is not in fact with drivers or the GPU, but rather Windows itself.

User reports of "Screen tearing" or "Screen glitches" often makes it hard to see how widespread the issue is as the generic terms of describing the issue due to lack of technical knowledge in describing exactly what is being displayed, however based on personal observance from friends and helpers alike on the [r/techsupport discord server](https://discord.gg/2EDwzWa), it appears to be more common than one may think. (I personally have not encountered this bug however I will admit.)

### What is DWM?
Desktop Window Manager (DWM) is Windows’ GPU compositor: it takes GPU-backed buffers (Direct3D/DXGI swap chains), composes and blends them, and presents the final desktop framebuffer to the display. DirectX provides the swap chains, textures, and GPU present path that DWM orchestrates and may promote to hardware overlay planes for direct scanout (i.e. display to screen).

[Chromium](https://www.chromium.org/chromium-projects/) and [Electron](https://www.electronjs.org/) render into Direct3D/DXGI swap chains from their renderer/GPU processes; DWM either composes those swap chains into the desktop or assigns them to overlay planes, so Chromium/Electron windows behave like native DirectX surfaces for presentation, timing, and input, basically DWM’s decisions about composition, overlays, and present scheduling directly affect their frame delivery, latency, and visible smoothness.

### Main issue
DWM is dynamically assigning and reassigning DirectX swap chains between standard composed flips and hardware overlay (Independent Flip) planes based on perceived frame rate and activity. 

Chromium/Electron apps like VS Code and Discord produce GPU-backed swap chains that can be low‑FPS while idle; when DWM’s minimum-frame-rate policy decides a surface is too slow it moves that swap chain off an overlay (or back onto one) causing the PresentMon “Composed: Flip” to “Hardware Composed: Independent Flip” oscillation. 

That back-and-forth changes presentation timing, can drop or duplicate frames during focus/input transitions, and produces visible stutters or responsiveness oddities. Firefox appears unaffected because it uses a different surface/path or swap-chain lifecycle that avoids the same overlay assignment behavior.

---
## Symptoms and Diagnosis
- Graphical glitches on Chromium based services (Discord, VSCode, Chromium browsers, etc.)
   - Parts of the interface being updated while the rest is frozen.
   - Update of the interface upon mouse cursor hover.
- Issue affects all GPUs, including iGPUs:
   - AMD, Intel and NVidia all present the same issue in the same way.
- Issue still persists / temporarily resolved despite the following attempted fixes:
   - Disabling of several graphics optimizations built into Windows:
      - Hardware Accelerated GPU Scheduling (HAGS)
      - Game Mode in Windows
      - Hardware Acceleration of services
   - DDU and reinstallation of drivers.
   - Disabling overlays of different kinds for Windows andd services:
      - Discord Overlays, Game overlays (XBox game bar, Steam Overlay, etc.), Multi-Plane Overlay (MPO), etc.
   - In-Place install of Windows and full Windows reinstalls.

## Potential Solutions
The key idea to potentially fix this is to disable DWM's minimum-FPS requirement for assigning swap chains to overlay planes, making the low-FPS chains likelier to remain on overlays. This will involve tinkering with the registry.

### Method 1: Saving as a .reg file
1. Open up notepad.
2. Copy and paste the following into the note file:

   ```
   Windows Registry Editor Version 5.00

   [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\DWM]
   "OverlayMinFPS"=dword:00000000
   ```
3. Save this `.txt` file as a `.reg` file by simply renaming the extension. Preferably name it as `DWM_Fix.reg`.
4. Run the `DWM_Fix.reg` file. You may have a UAC (User Account Control) dialogue popup.

After adding the key, open Task Manager, find Desktop Window Manager (dwm.exe), choose "End task". DWM will restart automatically and the overlay assignment thrash should stop; reboot if you prefer.

### Method 2: Using Regedit

{: .warning }
> *The registry is very powerful and allows you to change many things regarding how Windows operates, but it can be dangerous if you mess up adding keys or values to areas which do not belong. If you decide to do your own thing, you may end up with a broken Windows install which can only be fixed with a [reinstall of Windows](https://rtech.support/windows), unless you have backed the registry or have a System Restore point. Note that this also is no guarantee if you cannot access Windows to begin with if it is that broken.*

Open up registry, head to the following registry hive: 
- `HKLM\SOFTWARE\Microsoft\Windows\DWM`

In this registry hive, add a new `DWORD(32-bit)` entry:
- Name: `OverlayMinFPS`
- Value: `0` (Default)

After adding the key, open Task Manager, find Desktop Window Manager (dwm.exe), choose "End task". DWM will restart automatically and the overlay assignment thrash should stop; reboot if you prefer.

## Credits
Thanks to [Maliwolf on Reddit](https://www.reddit.com/r/Windows11/comments/1kgp7ar/cause_and_solution_to_windows_24h2_related/) for helping me make this Wiki entry. They are the primary source for this issue and potential fix.