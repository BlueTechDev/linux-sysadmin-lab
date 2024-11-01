# Creating a markdown file for the updated Web-server setup documentation

web_server_content = """
# Web Server and Pi-hole Configuration

## Overview
This document outlines the step-by-step configuration and management of Pi-hole for specific devices on the network, including custom DNS rules for blocking or allowing traffic to designated sites.

## Device Configuration
### 1. Setting Up DNS on Individual Devices
Manually configure each device to use the Pi-hole server as its DNS server (`192.168.1.111`).

#### iPhone
- **Settings > Wi-Fi**: Tap the `i` icon next to the connected network.
- **Configure DNS**: Select **Manual**, remove existing entries, and add `192.168.1.111`.
- Save changes.

#### Android
- **Settings > Network & Internet > Wi-Fi**: Tap the connected network.
- **Advanced > IP settings**: Change to **Static**.
- Set **DNS 1** to `192.168.1.111` and save.

#### Windows Laptop
- **Control Panel > Network and Internet > Network and Sharing Center**: Click **Change adapter settings**.
- Right-click the active network > **Properties**.
- Select **Internet Protocol Version 4 (TCP/IPv4)** > **Properties**.
- Enter `192.168.1.111` as the **Preferred DNS server** and save.

#### MacBook
- **System Preferences > Network**: Select the active network and click **Advanced**.
- **DNS Tab**: Add `192.168.1.111` and save.

### 2. Group Management for Device-Specific Rules
- Navigate to **Group Management > Groups** in the Pi-hole admin interface.
- Create groups:
  - **My Phone**
  - **Wife’s Phone**
  - **Work Laptops**
- Assign devices to their respective groups under **Group Management > Clients** by IP or MAC address.

### 3. Custom Block/Allow Rules
- Go to **Domain Management > Blacklist** or **Whitelist**.
- Example test: Block `target.com` for selected devices.
  - Add `target.com` to the **Blacklist** for the appropriate group.

### 4. Testing and Monitoring
- Test the setup by visiting blocked/allowed sites from configured devices.
- Check the **Query Log** to ensure the rules are being applied.
- Monitor the **Dashboard** for real-time statistics.

## Final Thoughts
With this configuration, you can customize DNS filtering and ad-blocking for each device, creating a more tailored network experience. Continue to fine-tune settings as needed and expand to more devices when ready.
"""

# Define the file path
file_path = "/mnt/data/Web-server-Updated.md"

# Write the content to the markdown file
with open(file_path, "w") as file:
    file.write(web_server_content)

file_path
