---
layout: default
title: Coding-Blog-guide-1 - WSL Basics
description: Introduction to WSL, basic operations and other useful information.
nav_exclude: false
has_children: false
parent: Coding-blog
grand_parent: Blog and personal opinions
# has_toc: false
search_exclude: true
last_modified_date: 2026-06-17
---

# Coding Blog - WSL Basics

This is a short guide in explaining how to set up and use WSL.

{: .no_toc }

{% include toc.md %}

## 1. What WSL Is and Why Use It

Windows Subsystem for Linux (WSL) lets you run a real Linux environment inside Windows, without dual booting or managing a full virtual machine. You get a Linux shell, packages, and tools, all while keeping your usual Windows desktop and apps.

For a typical Windows developer, WSL is a way to use Linux‑first tools (bash, git, language runtimes, package managers, build systems) right on the same machine you use for Visual Studio, VS Code, and browsers. For a Linux developer now on Windows, it gives you a familiar Linux userland and command‑line workflow, so you can treat WSL almost like a local dev server.

At a high level, WSL provides “Linux userland on Windows”—Linux distributions like Ubuntu and Debian run directly on top of Windows, but use Windows’ resources (CPU, memory, disk) and integrate with Windows apps. 

{: .info }
> There are two versions: WSL 1 and WSL 2; you’ll choose later, but you only need the names for now.

## 2. Requirements and Getting WSL Installed
Naturally you will need a Windows machine to run WSL, plus admin rights to enable WSL the first time. On most personal machines this is straightforward; on corporate machines, you may need IT approval especially if you lack admin access and rights.

### Installing WSL
For current Windows builds, the easiest way to install WSL is:
1. Open up **Windows Terminal** or **PowerShell** as **Administrator**.
2. Run:
    ```ps
    wsl --install
    ```

This turns on the WSL features, installs a default Linux distro ([which is Ubuntu if not pre-configured](https://learn.microsoft.com/en-us/windows/wsl/basic-commands#install)), and sets up WSL 2 if supported.

{: .important }
> **WSL is not being installed!**
>
>  If this does not work, you may first need to enable virtualization features in both Windows and BIOS. For Windows, press **Win + R**, type in `optionalfeatures.exe`, then scroll and tick the "**Virtual Machine Platform**" and "**Windows Subsystem for Linux**" boxes, and restart.

If you don't want Ubuntu and want another distribution instead, you can list available distros for download and delete the default distro that was installed (see the "Removing, Resetting and Cleaning Up WSL" section below):
```ps
wsl --list --online
wsl --install -d Fedora
```

Ubuntu is the recommended default for most developers: it's widely used, has strong documentation, and most examples assume it, in addition to very high compatibility with WSL. If you care about a specific ecosystem, you can pick Debian, Fedora, Kali, etc. instead from that list.

{: .note }
> The rest of the guide will assume you use Ubuntu as the main distro. Different distros may have different repositories and package managers available so ensure you adapt the commands accordingly.

On your first run of your distro:
- You will be prompted to create a Linux user and password; this is separate from your Windows account.
- Update packages so tools are up to date
    ```bash
    sudo apt update && sudo apt upgrade
    ```

This will provide you a clean, up-to-date base to work from before you start installing dev tools and runtimes.

### Which WSL version should you use?

{: .info }
> **WSL 2**
>
> WSL 2 uses a real Linux kernel inside a lightweight VM, which gives much better compatibility with Linux tools and services, and generally better performance on dev workloads that touch many files or rely on Linux system calls.
>
> It is the "normal Linux" experience with tight Windows integration.

{: .info }
> **WSL 1**
>
> WSL 1 runs Linux userland through a translation layer, avoiding the VM kernel and making it lighter on older hardware, but it doesn't support all Linux features and can be limiting for services, containers, and some tooling.

You can check your distros and versions with the following command (in powershell):

```ps
wsl -l -v
```

And change versions or defaults:

```ps
wsl --set-version <DistroName> 2
wsl --set-default-version 2
```

For nearly all modern development, be it web apps, databases, tooling, the simple guidance is use WSL 2 unless you have a specific reason not to (such as virtualization being disabled or restricted).

## 3. Basic WSL Usage (Shell, Commands, and Files)
You can start WSL in several ways:
- From the **Start menu**, click on your distro (e.g., "Ubuntu) or search it up using **Search**
- From Windows Terminal, you can run the default distro that's installed by running:
    ```ps
    wsl
    ```
- If you have multiple distros and want to launch a specific one, run:
    ```ps
    wsl -d <DistroName>
    ```

Inside WSL, you are in a Linux shell (usually `bash`). A few core commands that you will use constantly will be:
- `ls` – list files and directories.
- `cd` - change directory
- `pwd` - show current directory
- `mkdir` - create a directory
- `rm` remove files or directories (using `rm -r`)
- `cp` - copy files
- `mv` - move or rename files

On Ubuntu or Debian, you install packages with the package manager `apt`. Remember that different distros have different package managers, so refer to said package manager instructions depending on your distro of choice:
```bash
sudo apt install git
sudo apt install build-essential
sudo apt install <package name>
```

Your home directory is usually `/home/<user>`; that's where you should keep your projects and configuration.

The root (`/`) contains system directories like `/bin`, `/etc`, `/usr` which the distro manages. Usually you should leave these alone except when installing or configuring system tools.

### Windows-Linux Integration (Using editors and Explorer)
WSL is designed to integrate with your Windows tools rather than replace them. A common pattern usually is VS Code and WSL: In WSL, `cd` into your project folder and run:
```bash
code .
```
This opens VS Code on Windows, but connects it to your WSL environment through the `Remote-WSL` extension, so all commands, extensions, and terminals runs inside Linux while the UI runs on Windows.

To open your current WSL directory in Windows Explorer, you can run:
```bash
explorer.exe .
```
This is handy for quick file browsing, drag-and-drop, or interacting with tools that only understand Windows paths.

You can also run Windows executables from WSL, such as:
```bash
notepad.exe README.txt
```

This lets you mix Windows GUI apps with your Linux command-line workflow. Useful when you want to preview something in a Windows browser or editor but keep the dev stack in Linux.

Windows drives are mounted under `/mnt`, e.g. `/mnt/c` for the C: drive. You *can* work with code there, but for performance and correctness, especially with tools that do heavy I/O (build systems, databases, test runners), it's best to keep your main projects in the Linux filesystem (e.g., `/home/<user>/projects`)

### Code Example A (Simple): Develop and Compile in WSL
Here's a full, simple dev workflow using WSL and VS Code:
1. In WSL, create a project folder:
    ```bash
    mkdir my-project
    cd my-project
    ```
2. Open it in VSCode:
    ```bash
    code .
    ```
3. Install a language runtime. Lets go with an easy to start out language: Python (good for scripting or web stack)
    ```bash
    sudo apt install python3 python3-pip
    ```
    Create a `main.py` in VS Code:
    ```py
    print("Hello from WSL")
    ```
4. Run it from the WSL terminal:
    ```bash
    python3 main.py
    ```

If you are doing C/C++ or systems work, install the build tools instead:
```bash
sudo apt install build-essential
```

Next create `main.c`:
```c
#include <stdio.h>

int main() {
    printf("Hello from WSL in C!\n");
    return 0;
}
```

Then compile and run the code:
```bash
gcc main.c -o main
./main
```

This is the same pattern you will use on a Linux server or cloud VM: Linux packages and tools, source in `/home`, editor on Windows, consistent environments across machines.

### Code Example B (Advanced): Using Docker with WSL
Docker is just one advanced use case, but it's a good example of WSL integrating with broader dev tooling.

Docker Desktop for Windows can use WSL 2 as its backend, so containers run inside the WSL 2 environment while the Docker UI and settings live in Windows. This is simpler for most developers than installing Docker Engine directly into WSL.

A minimal path:
1. Confirm your distro is in fact using WSL 2 (Powershell):
    ```ps
    wsl -l -v
    ```
    If needed, switch:
    ```ps
    wsl --set-version <DistroName> 2
    ```
2. Install [**Docker Desktop for Windows**](https://docs.docker.com/desktop/setup/install/windows-install/) and enable integration for your WSL distro in its settings.
3. In WSL, test docker:
    ```bash
    docker run hello-world
    ```

If the test container runs, you have WSL and Docker working together. Disk usage and performance are generally good, but large images and volumes can consume space quickly; you can later move Docker/WSL storage to another drive if your C drive gets tight.

## 4. Management of WSL

### File System, Performance, and "Best Practices"
A few patterns will keep WSL smooth and fast:
- **Keep your active projects on the Linux filesystem**, typically under `/home/<user>`, not on `/mnt/c` (or D or any other drives). Linux file I/O is much faster and more reliable there; Windows-mounted drives are best treated as "shared storage" and not the primary workspace.
- Avoid running heavy builds, databases, or test suites directly on `/mnt/c` or other mounted drives. Instead, copy or clone repositories directly into `/home` and work there, using `/mnt/c` only to exchange files with Windows apps.

### Removing, Resetting, and Cleaning up WSL
To remove a specific distro (from Windows):
```ps
wsl --unregister <DistroName>
```

This completely deletes that Linux environment and all its files; export it first if you might need it again (see below).

### Moving WSL to Another Drive and Backups
Each WSL distro is stored as a virtual disk file (VHDX) under your user profile. If your system drive (C:) is getting full, or you want clearer backup and storage control, you can move a distro to another drive.

The usual export-unregister-import workflow (all in Windows) is:
1. Export:
    ```ps
    wsl --export Ubuntu D:\WSL\ubuntu.tar
    ```
2. Unregister the old instance (this deletes it, so make sure export succeeded):
    ```ps
    wsl --unregister Ubuntu
    ```
3. Import to the new location:
    ```ps
    wsl --import Ubuntu D:\WSL\ubuntu.tar --version 2
    ```

After the import, the distro's files live under `D:\WSL`, but you can still use it via `WSL -d Ubuntu` as usual. The same process doubles as a backup strategy: export to a safe location (another drive, external disk, etc.), and re-import it later on the same drive or another machine.

If you are using Docker Desktop with WSL, you can also point Docker's data storage to another drive in its settings, so container images and volumes don't grow on `C:\`.

## 5. Troubleshooting and Common Issues
Here's some basic commands to help you diagnose issues (from Windows):
```ps
wsl --status
wsl -l -v
wsl --shutdown
```

Common problems include:
- WSL won't start at all (often missing features or outdated Windows build).
- A distro running on WSL 1 when you expected WSL 2.
- Networking quirks after sleep, VPN changes, or firewall rules.

Simple fixes usually include:
- Run `wsl --shutdown` then restart your distro.
- Ensure that the **Windows Subsystem for Linux** and **Virtual Machine Platform** features are enabled and that virtualization is turned on in BIOS.
- Update Windows and your distro to current/latest versions.
- For deeper issues, you can check WSL and system logs as suggested in the [WSL FAQ](https://learn.microsoft.com/en-us/windows/wsl/faq) and [VS Code remote troubleshooting docs](https://code.visualstudio.com/docs/remote/troubleshooting).