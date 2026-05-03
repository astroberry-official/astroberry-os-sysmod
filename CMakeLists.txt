cmake_minimum_required(VERSION 2.8)
PROJECT(astroberry-os-sysmod NONE)

set (VERSION_MAJOR 3)
set (VERSION_MINOR 2)
set (VERSION_RELEASE 0)

set(CONFIG_INSTALL_DIR "/etc")
set(BOOT_INSTALL_DIR "/etc")
set(BIN_INSTALL_DIR "/usr/bin")

include_directories(${CMAKE_CURRENT_SOURCE_DIR})
include_directories(${CMAKE_CURRENT_BINARY_DIR})

configure_file(${CMAKE_CURRENT_SOURCE_DIR}/version.cmake ${CMAKE_CURRENT_BINARY_DIR}/version)

if (${CMAKE_SYSTEM_NAME} MATCHES "Linux")
	# Add APT repository
	install(FILES ${CMAKE_CURRENT_SOURCE_DIR}/files/apt/astroberry.gpg DESTINATION ${CONFIG_INSTALL_DIR}/apt/keyrings)
	install(FILES ${CMAKE_CURRENT_SOURCE_DIR}/files/apt/astroberry.sources DESTINATION ${CONFIG_INSTALL_DIR}/apt/sources.list.d)
	install(FILES ${CMAKE_CURRENT_SOURCE_DIR}/files/apt/astroberry-pin DESTINATION ${CONFIG_INSTALL_DIR}/apt/preferences.d)
	# Add polkit rules
	install(FILES ${CMAKE_CURRENT_SOURCE_DIR}/files/polkit/10-power-manager.rules DESTINATION ${CONFIG_INSTALL_DIR}/polkit-1/rules.d)
        install(FILES ${CMAKE_CURRENT_SOURCE_DIR}/files/polkit/10-file-manager.rules DESTINATION ${CONFIG_INSTALL_DIR}/polkit-1/rules.d)
        install(FILES ${CMAKE_CURRENT_SOURCE_DIR}/files/polkit/10-network-manager.rules DESTINATION ${CONFIG_INSTALL_DIR}/polkit-1/rules.d)
	install(FILES ${CMAKE_CURRENT_SOURCE_DIR}/files/polkit/10-synaptic.rules DESTINATION ${CONFIG_INSTALL_DIR}/polkit-1/rules.d)
	# Add reverse proxy config
        install(FILES ${CMAKE_CURRENT_SOURCE_DIR}/files/revproxy/Caddyfile DESTINATION ${CONFIG_INSTALL_DIR}/caddy)
	# Add system services
	install(FILES ${CMAKE_CURRENT_SOURCE_DIR}/files/services/vncserver.service DESTINATION ${CONFIG_INSTALL_DIR}/systemd/system)
	install(FILES ${CMAKE_CURRENT_SOURCE_DIR}/files/services/indiwebmanager.service DESTINATION ${CONFIG_INSTALL_DIR}/systemd/system)
	install(FILES ${CMAKE_CURRENT_SOURCE_DIR}/files/services/websockify.service DESTINATION ${CONFIG_INSTALL_DIR}/systemd/system)
        install(FILES ${CMAKE_CURRENT_SOURCE_DIR}/files/services/astroberry-manager.service DESTINATION ${CONFIG_INSTALL_DIR}/systemd/system)
        install(FILES ${CMAKE_CURRENT_SOURCE_DIR}/files/services/astroberry.service DESTINATION ${CONFIG_INSTALL_DIR}/avahi/services)
	# Add file sharing config
	install(FILES ${CMAKE_CURRENT_SOURCE_DIR}/files/filesharing/smb.conf DESTINATION ${CONFIG_INSTALL_DIR}/samba)
	# Add hotspot
        install(FILES ${CMAKE_CURRENT_SOURCE_DIR}/files/hotspot/Hotspot.nmconnection DESTINATION ${CONFIG_INSTALL_DIR}/NetworkManager/system-connections PERMISSIONS OWNER_READ OWNER_WRITE)
	# Add custom desktop config
        install(FILES ${CMAKE_CURRENT_SOURCE_DIR}/files/desktop/lightdm-gtk-greeter.conf DESTINATION ${CONFIG_INSTALL_DIR}/lightdm/lightdm-gtk-greeter.conf)
        install(FILES ${CMAKE_CURRENT_SOURCE_DIR}/files/desktop/xfce4-session.xml DESTINATION ${CONFIG_INSTALL_DIR}/xdg/xfce4/xfconf/xfce-perchannel-xml/xfce4-session.xml)
        install(FILES ${CMAKE_CURRENT_SOURCE_DIR}/files/desktop/xsettings.xml DESTINATION ${CONFIG_INSTALL_DIR}/xdg/xfce4/xfconf/xfce-perchannel-xml/xsettings.xml)
        install(FILES ${CMAKE_CURRENT_SOURCE_DIR}/files/desktop/default.xml DESTINATION ${CONFIG_INSTALL_DIR}/xdg/xfce4/panel/default.xml)
        install(FILES ${CMAKE_CURRENT_SOURCE_DIR}/files/desktop/xfce-applications.menu DESTINATION ${CONFIG_INSTALL_DIR}/xdg/menus)
	# Add cloud-init config
        install(FILES ${CMAKE_CURRENT_SOURCE_DIR}/files/cloudinit/meta-data DESTINATION ${BOOT_INSTALL_DIR}/firmware)
        install(FILES ${CMAKE_CURRENT_SOURCE_DIR}/files/cloudinit/user-data DESTINATION ${BOOT_INSTALL_DIR}/firmware)
        install(FILES ${CMAKE_CURRENT_SOURCE_DIR}/files/cloudinit/network-config DESTINATION ${BOOT_INSTALL_DIR}/firmware)
	# Add first boot init scripts
        install(FILES ${CMAKE_CURRENT_SOURCE_DIR}/files/firstboot/astroberry-os-init DESTINATION ${BIN_INSTALL_DIR})
        install(FILES ${CMAKE_CURRENT_SOURCE_DIR}/files/firstboot/astroberry-desktop-init DESTINATION ${BIN_INSTALL_DIR})
	# Add Astroberry OS version file
	install(FILES ${CMAKE_CURRENT_BINARY_DIR}/version DESTINATION ${CONFIG_INSTALL_DIR}/astroberry)
endif()
