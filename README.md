# OpenVPN Auto-Installer (IP Resilient)

This script allows you to quickly and securely set up an OpenVPN server on Debian, Ubuntu, CentOS, Fedora, and other major Linux distributions.

It is based on the excellent work of the [angristan/openvpn-install](https://github.com/angristan/openvpn-install) project.

## Key Feature: Resilience to Server IP Address Changes

This version of the script has been modified to be resilient to server IP address changes.

In many cloud or residential environments, a server's public IP address can change after a reboot or network event. This script solves that problem by **dynamically resolving the server's current public IP address every time you generate a new client `.ovpn` configuration file.**

This means if your server's IP changes, you don't need to reconfigure anything on the server. Simply run the script again, generate a new client profile, and it will automatically contain the new, correct IP address.

## Usage

### 1. Download the Script

Download the `openvpn-install.sh` script to your server.

```bash
curl -O https://github.com/heyaibi/openvpn-install/openvpn-install.sh
```

### 2. Make it Executable

Give the script execution permissions.

```bash
chmod +x openvpn-install.sh
```

### 3. Run the Installer

Run the script as root to begin the installation.

```bash
sudo ./openvpn-install.sh
```

The script will guide you through a few questions to configure your OpenVPN server and will generate your first client configuration file.

## After Installation

You can run the script again at any time to manage your OpenVPN server. A menu will appear with the following options:

*   **1) Add a new user**: Generates a new client `.ovpn` configuration file. This will use the server's current public IP address.
*   **2) Revoke an existing user**: De-authorizes a client certificate, preventing that user from connecting.
*   **3) Remove OpenVPN**: Uninstalls OpenVPN and removes all related configurations and firewall rules.
*   **4) Exit**: Closes the script.

## Unattended Installation

For automated deployments, you can run the script with environment variables. This will bypass all interactive prompts.

**Example:**

This command installs OpenVPN on port 49309, disables IPv6, and creates a passwordless client named `VPNClient`.

```bash
sudo AUTO_INSTALL=y PORT_CHOICE=2 PORT=49309 IPV6_SUPPORT=n CLIENT=VPNClient PASS=1 ./openvpn-install.sh
```

## Credits

This script is a modified version of the widely-used and trusted `openvpn-install` script created by **Angristan**. The original repository and documentation can be found here:

*   **Original Repository**: [https://github.com/angristan/openvpn-install](https://github.com/angristan/openvpn-install)

All credit for the core functionality, security best practices, and multi-distribution support goes to the original author and its contributors.
