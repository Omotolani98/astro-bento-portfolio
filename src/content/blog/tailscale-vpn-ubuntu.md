---
layout: ../../layouts/LayoutBlogPost.astro
title: "Setting Up Tailscale VPN on a Home Server"
description: "A simple guide to setting up Tailscale VPN to home servers in LAN environment"
pubDate: 2024-12-16
category: "tutorial"
---
# [![Tailscale Banner](https://via.placeholder.com/1000x300P)](https://tailscale.com)

# Setting Up Tailscale VPN on a Home Server

Easily configure secure, private access to your home server using Tailscale VPN. This guide will walk you through the installation, setup, and basic configuration of Tailscale.

---

## Table of Contents
- [Prerequisites](#prerequisites)
- [Step 1: Install Tailscale](#step-1-install-tailscale)
- [Step 2: Start Tailscale](#step-2-start-tailscale)
- [Step 3: Verify Connectivity](#step-3-verify-connectivity)
- [Step 4: Access Your Home Server Remotely](#step-4-access-your-home-server-remotely)
- [Step 5: Optional Configuration](#step-5-optional-configuration)
  - [Enable MagicDNS](#enable-magicdns)
  - [Set Up Subdomains for Services](#set-up-subdomains-for-services)

---

## Prerequisites

Before starting, ensure the following:
- **Operating System**: A Linux-based home server (e.g., Ubuntu, Debian).
- **Administrator Access**: You need `sudo` privileges on the server.
- **Tailscale Account**: A valid Tailscale account. Sign up [here](https://tailscale.com).

---

## Step 1: Install Tailscale

Install Tailscale on your home server with the following commands:

1. **Update Package Lists**:
   ```bash
   sudo apt update
   ```
2. **Install Tailscale**:
   ```bash
   curl -fsSL https://tailscale.com/install.sh | sh
   ```
3. **Confirm Installation**:
   Verify that Tailscale is installed:
   ```bash
   tailscale version
   ```

---

## Step 2: Start Tailscale

1. Start Tailscale and authenticate:
   ```bash
   sudo tailscale up
   ```
2. **Log In**:
   - After running the command, you'll be prompted to open a URL in your browser to log in to your Tailscale account.
   - Once logged in, your server will join your Tailscale network.

---

## Step 3: Verify Connectivity

1. **Get Your Tailscale IP**:
   ```bash
   tailscale ip
   ```
   This will return an IP in the `100.x.x.x` range, which is the private Tailscale network IP.

2. **Check Connection Status**:
   ```bash
   tailscale status
   ```

---

## Step 4: Access Your Home Server Remotely

To remotely access your home server from another device:
1. Install Tailscale on the remote device:
   - [Download Tailscale](https://tailscale.com/download) for Windows, macOS, Linux, Android, or iOS.
2. Log in using the same Tailscale account.
3. Use the Tailscale IP of your home server to connect:
   - Example for SSH:
     ```bash
     ssh username@100.x.x.x
     ```

---

## Step 5: Optional Configuration

### Enable MagicDNS

Enable **MagicDNS** to access your server using human-readable hostnames instead of IPs.

1. Open the Tailscale Admin Console:
   - [Tailscale Admin Console](https://login.tailscale.com/admin)
2. Navigate to **DNS Settings**.
3. Enable **MagicDNS**.

Now you can access your server via its Tailscale hostname:
```bash
ssh username@server-name.tailscale.net
```

---

### Set Up Subdomains for Services

You can use subdomains (e.g., `service.mydomain.com`) to access services hosted on your home server:
1. **Update Your DNS Records**:
   - Add an **A record** for the subdomain pointing to your Tailscale IP (`100.x.x.x`).
2. **Set Up a Reverse Proxy (Optional)**:
   - Use Nginx or Traefik to route traffic from the subdomain to specific services on your server.

Example Nginx configuration:
```nginx
server {
    server_name service.mydomain.com;

    location / {
        proxy_pass http://localhost:8080;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
    }
}
```

---

## Conclusion

You’ve successfully installed and configured Tailscale on your home server! Your server is now accessible securely from anywhere. For more advanced configurations, check the [Tailscale Documentation](https://tailscale.com/kb/).

---