# Pi-hole Setup on Raspberry Pi: A Step-by-Step Guide

## Introduction

Pi-hole is a network-wide ad blocker that acts as a DNS sinkhole, filtering out unwanted ads and improving your browsing experience. By blocking ads at the network level, Pi-hole not only makes your internet faster but also protects your privacy by preventing your devices from communicating with ad servers.

In this guide, we'll walk you through the steps to set up Pi-hole on a Raspberry Pi.

## Prerequisites

Before we start, ensure you have the following:

- A Raspberry Pi (any model will work, but a Raspberry Pi 3 or later is recommended)
- A microSD card (8GB or larger)
- A power supply for the Raspberry Pi
- An Ethernet cable (recommended) or Wi-Fi connection
- Access to your router’s admin interface
- A computer with SSH enabled (optional, but recommended)

## Step 1: Prepare the Raspberry Pi

1. **Download and Install Raspberry Pi OS**  
   - Download the Raspberry Pi Imager from the official [Raspberry Pi website](https://www.raspberrypi.org/software/).
   - Insert your microSD card into your computer.
   - Use the Raspberry Pi Imager to flash Raspberry Pi OS (Lite version is sufficient) onto your microSD card.
   - Once the flashing is complete, insert the microSD card into your Raspberry Pi.

2. **Boot the Raspberry Pi**  
   - Connect your Raspberry Pi to power and network (Ethernet recommended for stability).
   - If you're using Wi-Fi, you may need to configure the Wi-Fi connection by editing the `wpa_supplicant.conf` file on the SD card before booting.

3. **Access the Raspberry Pi via SSH**  
   - On your computer, open a terminal and connect to your Raspberry Pi using SSH:  
     ```bash
     ssh pi@<RaspberryPiIPAddress>
     ```
   - The default username is `pi` and the password is `raspberry`.

## Step 2: Install Pi-hole

1. **Update the System**  
   - Before installing Pi-hole, update your system packages:
     ```bash
     sudo apt update && sudo apt upgrade -y
     ```

2. **Install Pi-hole**  
   - Run the following command to install Pi-hole:
     ```bash
     curl -sSL https://install.pi-hole.net | bash
     ```
   - The installation script will guide you through the setup process. You’ll need to configure a few options:
     - **Choose your preferred DNS provider** (e.g., Google, OpenDNS, Cloudflare, etc.)
     - **Set a static IP address** for your Raspberry Pi (make sure it’s outside your router’s DHCP range)
     - **Select blocklists** to determine which ads and trackers to block (the default ones are usually sufficient)
     - **Install the web admin interface** to manage Pi-hole from your browser
    
       ![adlists](https://github.com/user-attachments/assets/54d72da7-1c25-4333-aa4e-31586f787634)


3. **Finalize the Setup**  
   - After the installation completes, Pi-hole will provide you with a summary of the setup, including the URL for the web interface and the admin password.
   - You can access the Pi-hole dashboard by navigating to `http://<RaspberryPiIPAddress>/admin` from any device on your network.
  
     ![dashhboard](https://github.com/user-attachments/assets/2868689a-6c95-41ae-96cf-99bffb8cbc36)


## Step 3: Configure Your Network

1. **Set Pi-hole as the Primary DNS Server**  
   - To ensure that all devices on your network use Pi-hole, set your router’s DNS server to the IP address of your Raspberry Pi. This can usually be done in the DHCP settings of your router’s admin interface.
   - Alternatively, you can manually configure individual devices to use Pi-hole as their DNS server.

2. **Test Pi-hole**  
   - To verify that Pi-hole is working, try visiting a site with a lot of ads (like [Here](https://d3ward.github.io/toolz/adblock.html)). You should notice that most ads are blocked.
   - You can also monitor DNS queries and blocked domains from the Pi-hole web interface.

## Optional: Set Up Pi-hole as DHCP Server

If your router doesn't allow you to change DNS settings, you can configure Pi-hole to act as your DHCP server:

1. **Enable DHCP on Pi-hole**  
   - Go to the Pi-hole web interface (`http://<RaspberryPiIPAddress>/admin`) and navigate to **Settings > DHCP**.
   - Enable DHCP and set a range for IP addresses that Pi-hole will assign.
   - Disable DHCP on your router.

2. **Reconnect Your Devices**  
   - Reconnect your devices to the network to ensure they obtain new IP addresses and use Pi-hole as their DNS server.

## Conclusion

Congratulations! You've successfully set up Pi-hole on your Raspberry Pi. Enjoy an ad-free, faster, and more secure browsing experience across your entire network. 

For further customization, you can explore additional blocklists, whitelist domains, or even integrate Pi-hole with other tools like Unbound for DNS over HTTPS.

Happy browsing!

![more data](https://github.com/user-attachments/assets/7b7d7647-0361-493a-9bca-f7f726ff0ee0)

![databases](https://github.com/user-attachments/assets/5320b723-86e7-4111-95b6-3b827499c281)

## References

- [Pi-hole Official Documentation](https://docs.pi-hole.net/)
- [Raspberry Pi OS Installation Guide](https://www.raspberrypi.org/documentation/installation/installing-images/)
