# Phase 1: Hardware & OS Setup
This section covers how to turn your laptop into a server.

---

## 1. Wipe the existing OS & Install Ubuntu
Since we want a lightweight server OS wipe ou the existing OS and install ubuntu. 

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

![Lid Switch Config](./assets/Lid%20switch%20config.png)

Then Save and Exit.

---
