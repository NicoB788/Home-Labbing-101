# Homelab Setup Tutorial

This tutorial will walk you through how to make the simplest form of a home server.

## Material Requirements
- Old PC / Old Laptop with a network port
- Internet connection
- Ethernet cable
  
## Knowledge requirements
- Linux basics
- How to remove and install an OS
- Basic networking skills
- Basic hardware knowledge

---
# This Tutorial walks you through the following:

- How to Install & Configure the server Os
- How Create a NAS to get network Acess
- How install a dashboard for your server
- How to create a Media server using Jellyfin
- How to make a network-wide adblocker for your network
- How to make a minecraft server

---

# Phase 1: Hardware & OS Setup
This section covers how to turn your laptop into a server.

---

## 1. Wipe the existing OS & Install Ubuntu
 There are many server OSs to choose from. I recommend you to use Ubuntu because Ubuntu Server LTS is beginner friendly
 and easy to use for general purposes. Ubuntu LTS is a headless OS hence a great learning opportunity to learn Linux basics.
[More about server OS](https://www.geeksforgeeks.org/operating-systems/what-is-a-server-os/) 

Since we want a lightweight server OS wipe out the existing OS and install ubuntu. 

### Steps:
* **Download the ISO image** [Here](https://ubuntu.com/download/server)
* **Flash the ISO:** Use [Rufus](https://rufus.ie/) on another PC.
* **Boot Menu:** Restart the laptop and tap `F12` or `F2` (This changes according to your laptop manufacturer).
* **Installation Type:** Select **"Erase disk and install Ubuntu."**

---

## 2. The "Lid Close" Hack
By default, a laptop sleeps when closed. To make it a server, laptop must functins even when the lid is closed.

**Run this command in the Terminal:**
```bash
sudo nano /etc/systemd/logind.conf
```
Find the following lines and remove the comments and change accordingly.
* HandleLidSwitch=suspend
* HandleLidSwitchExternalPower=ignore
* HandleLidSwitchDocked=ignore
* LidSwitchIgnoreInhibited=no

Your Terminal should look like this after step 2.

![Lid Switch Config](../assets/Lid%20switch%20config.png)

Then Save and Exit.

---

