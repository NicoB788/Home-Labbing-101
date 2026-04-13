# 🛠 Phase 1: Hardware & OS Setup
This section covers how to turn the physical laptop into a server.

---

## 1. Wipe Windows & Install Ubuntu
Since we want performance, we are removing Windows entirely. 

### Steps:
* **Flash the ISO:** Use [Rufus](https://rufus.ie/) on another PC.
* **Boot Menu:** Restart the laptop and tap `F12` or `F2`.
* **Installation Type:** Select **"Erase disk and install Ubuntu."**

---

## 2. The "Lid Close" Hack
By default, a laptop sleeps when closed. To make it a server, we must "break" this setting.

**Run this command in the Terminal:**
```bash
sudo nano /etc/systemd/logind.conf

