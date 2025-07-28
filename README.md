<!-- omit in toc -->
# WebTop
`webtop` ("web desktop") is a simple solution to run a Linux operating system and desktop environment (specifically: Debian 12 with the XFCE user interface) within your existing operating system, and interact with the Linux desktop in your browser (no VirtualBox / VMWare / VNC client necessary!). Your files are synchronized between the Linux instance and your current operating system via a shared `data/` folder.

<!-- omit in toc -->
# Table of Contents
- [Design and Rationale](#design-and-rationale)
- [Beginner Friendly Guide to `webtop`](#beginner-friendly-guide-to-webtop)
- [`webtop` for Advanced Users](#webtop-for-advanced-users)
  - [Requirements](#requirements)
  - [Installing and Running `webtop`](#installing-and-running-webtop)
- [Critical Usage Notes](#critical-usage-notes)
- [Troubleshooting Common Issues](#troubleshooting-common-issues)
  - [Error: failed to bind host port..](#error-failed-to-bind-host-port)
  - [Error: "Cannot connect to the Docker daemon"](#error-cannot-connect-to-the-docker-daemon)
  - [Audio does not work](#audio-does-not-work)


# Design and Rationale
Getting non-Linux users to run a Linux operating system isn't always easy. Installing multiple operating systems on the same machine is an involved process. Virtual machines (VMs) are sometimes slow, and it's hard to run them with equal features across both Windows (x86 machines) and Mac (ARM machines) (we've tried!). 

`webtop` is heavily based on [docker-webtop](https://github.com/linuxserver/docker-webtop), which is itself based on [KasmVNC](https://github.com/linuxserver/docker-baseimage-kasmvnc). KasmVNC is the primary technology that allows us to interact with the Linux desktop in a browser over [VNC](https://en.wikipedia.org/wiki/VNC). Our contributions are limited to modifications of the base images to make them appropriate for our use case.


# Beginner Friendly Guide to `webtop`
This section provides a beginner-friendly guide to installing and using `webtop`. 


**❗If you are new to Docker or Git, please click on the relevant OS logo below to access the installation guide for your operating system.**

[![Windows Logo](images/webtopinstallguide/assets-generic/windows-logo.svg)](webtopinstall-windows.md)
[![Mac Logo](images/webtopinstallguide/assets-generic/mac-logo.svg)](webtopinstall-mac.md)
[![Linux Logo](images/webtopinstallguide/assets-generic/linux-logo.svg)](webtopinstall-linux.md)

 If you are already familiar with these tools, you can skip to the [Advanced Users](#webtop-for-advanced-users) section.

# `webtop` for ✨Advanced Users✨
This section assumes you are familiar with the terminal, `git`, and Docker. 


**❗If you are new to these tools, please refer to the [beginner-friendly guide](#installing-and-using-webtop-for-your-os-beginner-friendly) above**.

### Requirements
- **Docker**: Ensure you have Docker installed and running on your system. You can download it from [Docker's official website](https://www.docker.com/).
- **Git**: Make sure you have Git installed. You can download it from [Git's official website](https://git-scm.com/downloads).
- **Terminal**: Familiarity with terminal commands is assumed. You will need to use the terminal (i.e., Command Prompt on Windows, Terminal on macOS, or bash on Linux) to run commands.

### Installing and Running `webtop`
1. Clone the repository to your local machine using `git clone git@github.com:learn-compsci/webtop.git`.

2. Navigate to the cloned repository folder in your terminal:
    ```bash
    cd webtop
    ```
    
3. Start `webtop` using Docker Compose:
    ```bash
    docker compose up
    ```

4. Open your browser (e.g., Chrome/Firefox/Safari) and go to `localhost:3000`. You should see a Linux desktop interface.
![desktop](images/desktop.png)

5. **Updating Webtop**: If we release a new version of `webtop`, you can update it by running the following commands in the `webtop` folder:
    ```bash
    docker compose pull
    docker compose build --no-cache
    ```

# 🚨Critical Usage Notes🚨
Before using `webtop`, please read the following important notes regarding the `webtop` environment:

- **Data Sharing** The files you create on `webtop` are mostly automatically shared/synced to the `data/` folder that should be created.

- **Data persistence**: The `webtop` environment only guarantees that files in your `webtop`'s home directory (`~/` i.e., `/config`) are retained on each reboot. All files in other locations might not be preserved on container shutdown.

- **System Wide Applications**: If you install applications system-wide, they may not be available the next time you start `webtop` (due to the above behavior). 
    - You can install applications locally (within `~/`), or use [proot-apps](https://github.com/linuxserver/proot-apps) to do this, but we try to install everything that you need from the start.

# 🔨Troubleshooting Common Issues🔨
This section provides solutions to common issues you might encounter while using `webtop`. 

---

### Error: failed to bind host port..
Ports are how applications communicate over the network, and each port can only be used by one application at a time. If you see an error like `failed to bind host port for 0.0.0.0:3000`, that means you might already have an application running on that port. 

**Solution:**  
- Go to the `docker-compose.yml` file in this folder. 
- Under `ports`, change the `3000:3000` to e.g., `3005:3000`, where `3005` is the new port number on your existing operating system. 
- Now you can use `localhost:3005` to access WebTop.

---

### Error: "Cannot connect to the Docker daemon"
A daemon is a background program that runs continuously and handles requests. If you see an error like `Cannot connect to the Docker daemon`, it usually means Docker is not running on your system.

**Solution:**  
- **Windows/Mac:** Open Docker Desktop and ensure it is running. You might have to restart your computer.
- **Linux:** Start Docker with `sudo systemctl start docker` or `sudo service docker start`.

---
### Audio does not work
Your browser will ask you for permission to use audio/camera/microphone each time you start `webtop`. If you do not allow it, audio will not work. Therefore, you have to enable audio in the browser tab that's running WebTop (each time). This is intentional.

**Solution:**  
- Click the tiny arrow in the middle left of the screen (it looks like a play button). This opens a bar at the top middle of the screen. 
- Click the speaker icon to enable audio.

