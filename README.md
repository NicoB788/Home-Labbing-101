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
  
# [Step 1: Install & setup OS](./OS_setup.md)
 There are many server OSs to choose from. I recommend you to use Ubuntu because Ubuntu Server LTS is beginner friendly
 and easy to use for general purposes. Ubuntu LTS is a headless OS hence a great learning opportunity to learn Linux basics.
[More about server OS](https://www.geeksforgeeks.org/operating-systems/what-is-a-server-os/) 

---

# Step 2: Setting up the NAS (Network Access)
Creating a NAS is not strictly required but its way easier to access and manage your storage.

## 1. Install Samba
Samba is the software that allows Linux to share files with Windows and Mac.

**Run this commands to install it:**
```bash
sudo apt update && sudo apt install samba -y
```

Create a shared folder

```bash
mkdir /media/myfiles
```

Change the permission

```bash
sudo chown $USER: /media/myfiles
```

Change the samba configuration file

```bash
sudo nano /etc/samba/smb.conf
```
paste the following code block at the end of the file.

```bash
[myfiles]
  path = /media/myfiles
  writeable=yes
  public=no
```
your SMB configuration shold look like following

![Samba config](./assets/samba_Config.png)
