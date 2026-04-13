---

# Setting up the NAS (Network Access)
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

![Samba config](../assets/samba_Config.png)

## 2. Set credentials for NAS

```bash
sudo smbpasswd -a YOUR_USERNAME
sudo systemctl restart smbd
```

## 3. Ways to access your NAS

### 1. Mapping the NAS in windows

  To make your server easy to use, we will map it as a "Network Drive." This makes it appear right next to your "C:" drive in File Explorer.

 ### Instructions:
1. Open **File Explorer** on your Windows PC.
2. Click on **This PC** in the left sidebar.
3. In the top menu bar, click **Map network drive** (you might need to click the three dots `...` to find it).
   
   ![Windows map](../assets/map_network.png)
   
5. **Drive Letter:** Choose any letter (e.g., **Z:**).
6. To find your IP address use
   
   ``` bash
   ifconfig 
7. **Folder:** Type your server path: `\\192.168.1.XX\MyNAS` 
8. Make sure **"Reconnect at sign-in"** is checked.s
10. Click **Finish**.

> [!TIP]
> If it asks for credentials, use the username and the **Samba password** you created in Phase 3.

## 2. Remote access with SSh protocol

Since this is a server, we don't want to use the laptop's keyboard. We can access the server remotely from 
any machine within the network using **SSH**.
SSH (Secure Shell) allows you to control your laptop server's terminal from any other computer on your network.

### Instructions

1. Open the terminal on your server and type the following commands

   ```bash
   sudo apt update && sudo apt install openssh-server -y
   ```

2. Check if it's running

   ``` bash
   sudo systemctl status ssh
   ```
   your terminal should look like this if its running.

    ![ssh](../assets/ssh.png)
   
4. From your Windows PowerShell or Mac Terminal, type:
```bash
ssh username@192.168.1.XX
```

---

# Step 3 : Setting up a Dashboard for the Server

  ![Casa_Os](../assets/casa_OS02.png)

## Instructions
1. Go to [This](https://casaos.zimaspace.com/) website and copy the command
2. paste the command in your server terminal and run it

To access the Dashboard Type your server's IP Address in the browser.
you will get a sign up screen this is a one time sign up.



