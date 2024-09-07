i# VPN and proxy configuration in Linux

## 1. VPN Configuration

VPNs (Virtual Private Networks) provide secure, encrypted connections over public networks. There are several VPN protocols and clients available for Linux.

### OpenVPN:
OpenVPN is one of the most popular and secure VPN protocols. To set it up:

- 1. Install OpenVPN:
`sudo apt install openvpn`

- 2. Obtain configuration files from your VPN provider.
Varies on each provider

- 3. Connect to the VPN:
`sudo openvpn --config /path/to/your/config.ovpn`

- 4. For automatic connection, create a systemd service:
`sudo nano /etc/systemd/system/openvpn.service`
- Add the following content:
```
[Unit]
Description=OpenVPN connection to YOUR_VPN
After=network.target

[Service]
ExecStart=/usr/sbin/openvpn --config /path/to/your/config.ovpn
Restart=always

[Install]
WantedBy=multi-user.target
```

Enable and start the service:
- `sudo systemctl enable --now openvpn.service` # Starts OpenVPN right "now" and "enable"s it on next boot as well
- `sudo systemctl start openvpn.service` # Just "start"s OpenVPN for the current boot.


### WireGuard:
WireGuard is a newer, faster VPN protocol. To set it up:

- a. Install WireGuard: `sudo apt install wireguard`

- b. Create a configuration file: `sudo nano /etc/wireguard/wg0.conf`
 -Add your WireGuard configuration details specific to your vendor.

- c. Start the WireGuard connection:
- sudo wg-quick up wg0` 

- d. To "enable" automatic connection on boot and right "now":
- `sudo systemctl enable  --now wg-quick@wg0`

### Built-in VPN clients:
Many Linux distributions include built-in VPN clients in their network managers, supporting protocols like OpenVPN, L2TP/IPsec, and PPTP.

## 2. Proxy Configuration

Proxies route your traffic through an intermediary server. There are several ways to configure proxies in Linux:

### Environment variables:
Set these variables in your shell configuration file (e.g., ~/.bashrc):

```
export http_proxy="http://proxy_server:port"
export https_proxy="http://proxy_server:port"
export ftp_proxy="http://proxy_server:port"
export no_proxy="localhost,127.0.0.1,::1"
```

### System-wide proxy settings:
For GNOME-based systems:
- a. Open Settings > Network > Network Proxy
- b. Choose "Manual" and enter your proxy details

### For KDE-based systems:
- a. Open System Settings > Network Settings > Proxy
- b. Choose "Manual" and enter your proxy details

### Application-specific proxy settings:
Many applications have their own proxy settings. For example:

- Firefox: Preferences > Network Settings > Configure Proxy Access to the Internet
- Chrome: Settings > Advanced > System > Open your computer's proxy settings

### Command-line tools:
Use proxychains to route terminal commands through a proxy:

#### 1. Install proxychains:
`sudo apt install proxychains`

#### 2. Configure proxychains:
`sudo nano /etc/proxychains.conf`
Add your proxy server details.

#### 3. Use proxychains:
`proxychains command_to_run`

### SOCKS proxy with SSH:
Create a SOCKS proxy using SSH:
- `ssh -D 1080 -f -C -q -N username@remote_host`
- Then configure applications to use SOCKS5 proxy at 127.0.0.1:1080.

## 3. Testing and Verification

To verify your VPN or proxy configuration:

- Check your IP address:
`curl ifconfig.me`

- DNS leak test:
`dig +short myip.opendns.com @resolver1.opendns.com`

- WebRTC leak test (in browsers)

- Use tools like ipleak.net or dnsleak.com

## 4. Security Considerations

- Keep your VPN client and system updated
- Use strong authentication methods (e.g., certificates for OpenVPN)
- Be cautious with free VPN or proxy services
- Consider using a kill switch to prevent traffic leaks if the VPN disconnects

## 5. Troubleshooting

- Check logs: `journalctl -u openvpn` or `journalctl -u wg-quick@wg0`
- Verify DNS settings
- Ensure correct permissions on configuration files
- Check for conflicting network settings