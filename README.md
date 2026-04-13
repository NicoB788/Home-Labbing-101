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
your SMB configuration shold look like this

![Samba config](./assets/samba_Config.png)

## 2. Set credentials for NAS

```bash
sudo smbpasswd -a YOUR_USERNAME
sudo systemctl restart smbd
```

### Ways to access your NAS

1.Mapping the NAS in windows

To make your server easy to use, we will map it as a "Network Drive." This makes it appear right next to your "C:" drive in File Explorer.

## Instructions:
1. Open **File Explorer** on your Windows PC.
2. Click on **This PC** in the left sidebar.
3. In the top menu bar, click **Map network drive** (you might need to click the three dots `...` to find it).
4. **Drive Letter:** Choose any letter (e.g., **Z:**).
5. **Folder:** Type your server path: `\\192.168.1.XX\MyNAS`
6. Make sure **"Reconnect at sign-in"** is checked.
7. Click **Finish**.

> [!TIP]
> If it asks for credentials, use the username and the **Samba password** you created in Phase 3.




