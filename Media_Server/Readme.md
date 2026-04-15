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
   
![Jellyfin](./assets/jelllyfin.png)
   
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
  <img src="./Diagrams/LAN_network.png" alt="Corrected Jellyfin LAN Streaming Diagram" width="72%" />
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
  <img src="./Diagrams/Tunnel.png" alt="Corrected Jellyfin LAN Streaming Diagram" width="90%" />
</p>
  
---

# Cloudflare Tunnel

- Cloud flare Tunnels acts as a secured connection between your private network and the global network.
- Cloudflare tunnel builds a outbound connection eliminating the need to open ports or port forwarding.
- In order to implement a Cloud tunnel you need to buy a Domain.
- Cloudflare also allows you to buy Domains.
- You can secure a cheap domain name if you buy a .uk domain.

---

# Cloudflare Tunnel (cloudflared) Docker Deployment

This repository contains the configuration to run a Cloudflare Tunnel connector within a Docker container. Using Docker ensures a clean installation and easy updates for your home server gateway.

## Prerequisites

- **Docker** and **Docker Compose** installed on Ubuntu.
- A **Cloudflare account** with a domain pointed to Cloudflare DNS.
- A **Tunnel Token** from the Cloudflare Dashboard.

---

##  Step 1: Obtain Your Tunnel Token

1.  Log in to the [Cloudflare Zero Trust Dashboard](https://dash.cloudflare.com/).
2.  Navigate to **Networks** > **Tunnels**.
3.  Click **Create a Tunnel** (or select an existing one).
4.  Choose **Cloudflared** as the connector.
5.  Select **Docker** as the environment.
6.  Copy the token string provided in the command (the long string of characters after `--token`).

---

## Step 2: Project Setup

On your Ubuntu server, create a dedicated directory for the tunnel to keep your configuration organized.

```bash
mkdir -p ~/docker/cloudflared
cd ~/docker/cloudflared
```
Store your token in a hidden .env file to keep your docker-compose.yml clean and secure

```bash
nano .env
```

Paste the following (replace with your actual token):
```Code snippet
TUNNEL_TOKEN=your_unique_token_string_here
```

## Step 3: Create Docker Compose

Create the docker-compose.yml file:
```bash
nano docker-compose.yml
```

Paste the following configuration into the editor, then save and exit (Ctrl+O, Enter, Ctrl+X):
```YAML
services:
  tunnel:
    container_name: cloudflared-tunnel
    image: cloudflare/cloudflared:latest
    restart: unless-stopped
    environment:
      - TUNNEL_TOKEN=${TUNNEL_TOKEN}
    command: tunnel --no-autoupdate run
```

Launch the Tunnel
```bash
docker compose up -d
```

Verify Status
```bash
sudo docker ps
```

If its running your docker container should look like this

![docker](./assets/docker_ps.png)

## Step 4: Add Jellyfin to your Tunnel

First, configure your Cloudflare Tunnel to route traffic to your Jellyfin instance.

1. Go to the [Cloudflare Zero Trust Dashboard](https://one.dash.cloudflare.com/).
2. Navigate to **Networks** > **Tunnels**.
3. Click on your active tunnel and select **Configure**.
4. Go to the **Public Hostname** tab and click **Add a public hostname**.
5. Fill out the routing details:
   - **Subdomain:** e.g., `jellyfin`, `tv`, `media`
   - **Domain:** Select your domain from the dropdown.
   - **Service Type:** `HTTP`
   - **URL:** Enter your Jellyfin server's local address:
     - *If Jellyfin is in the same Docker network:* `jellyfin:8096`
     - *If Jellyfin is installed directly on your Ubuntu host:* `192.168.1.X:8096` (your server's local IP).
6. Click **Save hostname**.


## Step 5: Configure Jellyfin for the Reverse Proxy

Finally, configure Jellyfin to recognize that it is being accessed through a secure external tunnel.

1. Log in to your Jellyfin web interface locally (e.g., `http://192.168.1.X:8096`).
2. Go to **Dashboard** > **Networking**.
3. Scroll down to the **Published Server URIs** setting.
4. Enter your public URL exactly as you set it up (e.g., `https://jellyfin.yourdomain.com`).
5. Ensure the **Allow remote connections to this server** box is checked.
6. Click **Save** at the bottom of the page.

🎉 **Done!** You can now open the Jellyfin app on any device, enter your secure `https://` URL, and stream your media from anywhere.
