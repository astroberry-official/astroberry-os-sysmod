cmake_minimum_required(VERSION 3.16)
PROJECT(astroberry-os-sysmod NONE)

set (VERSION_MAJOR 3)
set (VERSION_MINOR 2)
set (VERSION_RELEASE 0)

set(BOOT_INSTALL_DIR "/boot/firmware")
set(CONFIG_INSTALL_DIR "/etc")
set(BIN_INSTALL_DIR "/usr/bin")

include_directories(${CMAKE_CURRENT_SOURCE_DIR})
include_directories(${CMAKE_CURRENT_BINARY_DIR})

configure_file(${CMAKE_CURRENT_SOURCE_DIR}/version.cmake ${CMAKE_CURRENT_BINARY_DIR}/version)

if (${CMAKE_SYSTEM_NAME} MATCHES "Linux")

	# First boot init scripts
	install(FILES ${CMAKE_CURRENT_SOURCE_DIR}/files/usr/bin/astroberry-os-init DESTINATION ${BIN_INSTALL_DIR})

	# Cloud-init config files
	install(FILES ${CMAKE_CURRENT_SOURCE_DIR}/files/boot/firmware/meta-data DESTINATION ${BOOT_INSTALL_DIR})
	install(FILES ${CMAKE_CURRENT_SOURCE_DIR}/files/boot/firmware/user-data DESTINATION ${BOOT_INSTALL_DIR})
	install(FILES ${CMAKE_CURRENT_SOURCE_DIR}/files/boot/firmware/network-config DESTINATION ${BOOT_INSTALL_DIR})
	install(FILES ${CMAKE_CURRENT_SOURCE_DIR}/files/etc/cloud/cloud.cfg.d/99-astroberry.cfg DESTINATION ${CONFIG_INSTALL_DIR}/cloud/cloud.cfg.d)

	# Hotspot
	install(FILES ${CMAKE_CURRENT_SOURCE_DIR}/files/etc/NetworkManager/system-connections/Hotspot.nmconnection DESTINATION ${CONFIG_INSTALL_DIR}/NetworkManager/system-connections
		PERMISSIONS OWNER_READ OWNER_WRITE)

	# Caddy config file
	install(FILES ${CMAKE_CURRENT_SOURCE_DIR}/files/etc/caddy/Caddyfile DESTINATION ${CONFIG_INSTALL_DIR}/caddy)

	# Samba config file
	install(FILES ${CMAKE_CURRENT_SOURCE_DIR}/files/etc/samba/smb.conf DESTINATION ${CONFIG_INSTALL_DIR}/samba)

	# Polkit rules
	install(FILES ${CMAKE_CURRENT_SOURCE_DIR}/files/etc/polkit-1/rules.d/99-astroberry-os.rules DESTINATION ${CONFIG_INSTALL_DIR}/polkit-1/rules.d)

	# System services
	install(FILES ${CMAKE_CURRENT_SOURCE_DIR}/files/etc/systemd/system/astroberry-desktop-web.service DESTINATION ${CONFIG_INSTALL_DIR}/systemd/system)
	install(FILES ${CMAKE_CURRENT_SOURCE_DIR}/files/etc/systemd/system/astroberry-desktop-vnc.service DESTINATION ${CONFIG_INSTALL_DIR}/systemd/system)
	install(FILES ${CMAKE_CURRENT_SOURCE_DIR}/files/etc/systemd/system/astroberry-indiwebmanager.service DESTINATION ${CONFIG_INSTALL_DIR}/systemd/system)
	install(FILES ${CMAKE_CURRENT_SOURCE_DIR}/files/etc/systemd/system/astroberry-websockify.service DESTINATION ${CONFIG_INSTALL_DIR}/systemd/system)

	# Avahi services
	install(FILES ${CMAKE_CURRENT_SOURCE_DIR}/files/etc/avahi/services/astroberry.service DESTINATION ${CONFIG_INSTALL_DIR}/avahi/services)

	# Lightdm
	install(FILES ${CMAKE_CURRENT_SOURCE_DIR}/files/etc/lightdm/lightdm-gtk-greeter.conf DESTINATION ${CONFIG_INSTALL_DIR}/lightdm)

	# XFCE
	install(FILES ${CMAKE_CURRENT_SOURCE_DIR}/files/etc/xdg/xfce4/xfconf/xfce-perchannel-xml/xfwm4.xml DESTINATION ${CONFIG_INSTALL_DIR}/xdg/xfce4/xfconf/xfce-perchannel-xml)
	install(FILES ${CMAKE_CURRENT_SOURCE_DIR}/files/etc/xdg/xfce4/xfconf/xfce-perchannel-xml/xfce4-desktop.xml DESTINATION ${CONFIG_INSTALL_DIR}/xdg/xfce4/xfconf/xfce-perchannel-xml)
	install(FILES ${CMAKE_CURRENT_SOURCE_DIR}/files/etc/xdg/xfce4/xfconf/xfce-perchannel-xml/xfce4-session.xml DESTINATION ${CONFIG_INSTALL_DIR}/xdg/xfce4/xfconf/xfce-perchannel-xml)
	install(FILES ${CMAKE_CURRENT_SOURCE_DIR}/files/etc/xdg/xfce4/xfconf/xfce-perchannel-xml/xsettings.xml DESTINATION ${CONFIG_INSTALL_DIR}/xdg/xfce4/xfconf/xfce-perchannel-xml)
	install(FILES ${CMAKE_CURRENT_SOURCE_DIR}/files/etc/xdg/xfce4/panel/default.xml DESTINATION ${CONFIG_INSTALL_DIR}/xdg/xfce4/panel)
	install(FILES ${CMAKE_CURRENT_SOURCE_DIR}/files/etc/xdg/menus/xfce-applications.menu DESTINATION ${CONFIG_INSTALL_DIR}/xdg/menus)

	# Text console banners
	install(FILES ${CMAKE_CURRENT_SOURCE_DIR}/files/etc/update-motd.d/20-astroberry-os DESTINATION ${CONFIG_INSTALL_DIR}/update-motd.d)
	install(FILES ${CMAKE_CURRENT_SOURCE_DIR}/files/etc/issue.d/AstroberryOS.issue DESTINATION ${CONFIG_INSTALL_DIR}/issue.d)

	# Astroberry OS version file
	install(FILES ${CMAKE_CURRENT_BINARY_DIR}/version DESTINATION ${CONFIG_INSTALL_DIR}/astroberry)

endif()
