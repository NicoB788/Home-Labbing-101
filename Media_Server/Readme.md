# Setting up Jellyfin Media Server
Jellyfin is a free, open-source media system that lets you stream all your movies and TV shows from your laptop server to any device (Phone, TV, or Tablet).

## 1. Install Jellyfin
The easiest way to install Jellyfin on Ubuntu is using their official repository script. Run this via SSH:

```bash
curl [https://repo.jellyfin.org/install-deb.sh](https://repo.jellyfin.org/install-deb.sh) | sudo bash
```
Since we have setup Casa OS you can download jellyfin from the Casa OS appstore

## Instructions
1. Click the jellyfin icon on casa OS and make an account.
2. Add your movies Folder to the jellyfin media library
   
![Jellyfin](../assets/jelllyfin.png)
   
4. To access Open your browser and type
   
   ```bash
   http://192.168.1.XX:8096\
   ```

## Hardware accelaratioon

**Since you are using a laptop, you can use the built-in graphics to help the server stream without the CPU getting too hot.**
## Instructions

1. Go to Dashboard > Playback.
2. Under Hardware Acceleration, select Intel QuickSync (QSV) or VA-API.

you're now a Proud owner of a Media Server !

---
# Accessing the Media server outside your Network

To access your jellyfin server from another network first you need to understand 
How your server acts within your private network.

Up until now we have kept our server inside our private network. You can only access your jellyfin server
if you are in the same network as the server. All your media is shared via LAN connection.

<p align="center">
  <img src="../Diagrams/LAN_network.png" alt="Corrected Jellyfin LAN Streaming Diagram" width="72%" />
</p>
 
- In order to access the jellyfin server from another network we need to make a connection from
  Global network to our home network.
  
There are few ways to do this.

1. Port forwarding
2. VPN
3. Reverse Proxy + Domain Name
4. Cloud Tunnel
       
- In this tutorial i will guide you how to do this with a **Cloud tunnel**

# This is how your Network looks after implementing a Tunnel.

<p align="center">
  <img src="../Diagrams/Tunnel.png" alt="Corrected Jellyfin LAN Streaming Diagram" width="72%" />
</p>
  
---

# Cloudflare Tunnel

- Cloud flare Tunnels acts as a secured connection between your private network and the global network.
- Cloudflare tunnel builds a outbound connection eliminating the need to open ports or port forwarding.
- In order to implement a Cloud tunnel you need to buy a Domain.
- Cloudflare also allows you to buy Domains.
- You can secure a cheap domain name if you buy a .uk domain.
