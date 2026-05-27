# astroberry-os-sysmod
System mods for Astroberry OS.

## List of mods

- First boot / Cloud-init
  - meta-data, user-data, network-config
  - astroberry-os-init invoked on first boot by cloud-init

- Wireless network
  - Preset wireless regulatory domain
  - Setup Hotspot

- XFCE desktop
  - Install backgrounds, logos, icons
  - Customize login greeter
  - Fix for low desktop performance on headless system
  - Customize GTK settings
  - Enable dark mode for panels
  - Customize panels
  - Customize menu layout

- Services
  - Caddy as web frontend service
  - TigerVNC services for web desktop and VNC access
  - Websockify for web desktop
  - INDI Web Manager as a middle-ware for Astroberry Manager
  - GPSD service for GPS devices
  - SMB File sharing
  - Zeroconf/Avahi

- Polkit user permissions for XFCE
  - Manage drives
  - Configure network connections
  - Power off and reboot
  - Use Synaptic package manager
  - Update already installed software
  - Set system clock, hostname,locale,keyboard,date/time without prompting

- Other tweaks
  - Custom system banners for text console
  - Basic system dependencies
  - Some salt and pepper