# Fortigate Basic Setup
![Imgur](https://imgur.com/K33rli9)

## Step 1: Connections

![Imgur](https://imgur.com/DiHQAIn)
1. Connect your computer to the FortiGate’s LAN port 1 via an Ethernet cable.
2. Connect the WAN port of the FortiGate to the ISP modem.
3. Open a web browser and enter the default IP address of the FortiGate (`https://192.168.1.99`).
4. Log in using the default credentials:
   - **Username:** `admin`
   - **Password:** (leave blank)
5. Change the password when prompted.


## Step 2: Configure Network Interfaces (WAN and LAN)

### A. Configure WAN Interface

![Imgur](https://imgur.com/DygodHf)

1. Go to `Network` > `Interfaces` and select the WAN interface (WAN 1 or 2) under Physical.
2. Set **Role** as WAN and **Addressing mode** to either `Manual` or `DHCP`. Most home networks use DHCP unless a static IP is purchased from the ISP.
3. If `DHCP` is selected, the DNS and gateway are acquired from the ISP. If `Manual`, the IP address, subnet mask, and gateway will be populated automatically.
4. Disable “Override internal DNS” if you prefer to use public DNS servers. Specify them under `Network` > `DNS` (e.g., Google DNS `8.8.8.8` or Cloudflare DNS `1.1.1.1`).
5. Select your preference for administrative access.
   

### B. Configure the LAN Interface

![Imgur](https://imgur.com/yG9SWb9)
![Imgur](https://imgur.com/xhHDwFz)

1. Set **Role** to LAN.
2. Enable **DHCP Server** and use Manual mode to set the IP address and subnet mask for the LAN interface (e.g., `192.168.1.1/24`).
3. Select the necessary administrative access methods (e.g., HTTPS, SSH, Ping).
4. Set the DHCP address range (e.g., `192.168.1.2` to `192.168.1.250`).
5. Set the **Default Gateway** to the interface IP (e.g., `192.168.1.1`).
6. Choose the DNS server option: “same as system DNS” or specify your preference.
7. **Advanced Options:**
   - Select **Server** as mode.
   - Choose the NTP server option: system NTP or a specific NTP server.
   - Adjust the DHCP lease time (default is 604800 seconds, or 7 days).
   - Add address reservations for your devices manually or from the DHCP client list.
   - Enable “device detection” to view connected devices under “User & Device,” useful for troubleshooting.

## Step 3: Create IPv4 Policy for NAT

To allow internal devices to access the internet and vice versa for external users, set up NAT policies to translate private IP addresses from LAN to public IP addresses for outbound traffic and vice versa for inbound traffic. Ensure your router is in Access Point (AP) mode, Bridge mode, or has DHCP disabled to avoid Fortigate and the router performing NAT simultaneously(Double NAT).

![imgur](https://imgur.com/vhybhn0)

1. Navigate to `Policy & Objects` > `IPv4 Policy`.
2. Click `Create New` and name it (e.g., Outbound NAT).
   - **Incoming Interface:** Select internal or VLAN if created.
   - **Outgoing Interface:** Select your WAN interface (e.g., `wan1`).
   - **Source:** Specify the source address or range (e.g., all or specific subnet like `192.168.1.0/24`).
   - **Destination:** Specify the destination address or range (e.g., all).
   - **Service:** Select the allowed services (e.g., ALL).
   - **Action:** Set to Accept.
   - **NAT:** Enable NAT.
   - Check “Use Outgoing Interface Address” to use the WAN interface IP for NAT.
  
  To be continued
