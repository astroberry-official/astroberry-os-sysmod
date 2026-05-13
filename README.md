# astroberry-os-sysmod
Custom system mods for vanilla Raspberry Pi OS for Astroberry OS.

## List of mods

- Distro config directory
  - Add Astroberry OS config directory
  - Add Astroberry OS version file

- Polkit for XFCE
  - Enable members of netdev group to edit network connections
  - Enable members of sudo group to manage packages
  - Enable members of sudo group to reboot and shutdown
  - Enable members of plugdev group to mount and eject external drives

- Systemd services
  - Setup TigerVNC service
  - Setup INDI Web Manager service
  - Setup Websockify service
  - Setup Astroberry Manager service

- Network services
  - Setup file sharing
  - Enable zeroconf/avahi

- XFCE desktop
  - Customize login greeter
  - Fix vnc slow down on headless system: xfwm4 --compositor=off --vblank=off --replace
  - Customize GTK settings
  - Enable dark mode for panels
  - Customize panel 1
  - Customize menu layout

- Cloud-init
  - meta-data
  - user-data
  - network-config

- Wireless network
  - Set wireless regulatory domain
  - Configure Hotspot

- Other tweaks
  - Add astroberry-os-init invoked on first boot by cloud-init
  - Remove astrodmx from top level menu
