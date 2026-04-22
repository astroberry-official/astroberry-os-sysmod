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
        install(FILES ${CMAKE_CURRENT_SOURCE_DIR}/files/astroberry.sources DESTINATION ${CONFIG_INSTALL_DIR}/apt/sources.list.d)
	install(FILES ${CMAKE_CURRENT_SOURCE_DIR}/files/astroberry.gpg DESTINATION ${CONFIG_INSTALL_DIR}/apt/keyrings)
        install(FILES ${CMAKE_CURRENT_SOURCE_DIR}/files/astroberry-pin DESTINATION ${CONFIG_INSTALL_DIR}/apt/preferences.d)
	install(FILES ${CMAKE_CURRENT_SOURCE_DIR}/files/10-power-manager.rules DESTINATION ${CONFIG_INSTALL_DIR}/polkit-1/rules.d)
        install(FILES ${CMAKE_CURRENT_SOURCE_DIR}/files/10-file-manager.rules DESTINATION ${CONFIG_INSTALL_DIR}/polkit-1/rules.d)
        install(FILES ${CMAKE_CURRENT_SOURCE_DIR}/files/10-network-manager.rules DESTINATION ${CONFIG_INSTALL_DIR}/polkit-1/rules.d)
	install(FILES ${CMAKE_CURRENT_SOURCE_DIR}/files/10-synaptic.rules DESTINATION ${CONFIG_INSTALL_DIR}/polkit-1/rules.d)
        install(FILES ${CMAKE_CURRENT_SOURCE_DIR}/files/Caddyfile DESTINATION ${CONFIG_INSTALL_DIR}/caddy)
	install(FILES ${CMAKE_CURRENT_SOURCE_DIR}/files/vncserver.service DESTINATION ${CONFIG_INSTALL_DIR}/systemd/system)
	install(FILES ${CMAKE_CURRENT_SOURCE_DIR}/files/indiwebmanager.service DESTINATION ${CONFIG_INSTALL_DIR}/systemd/system)
	install(FILES ${CMAKE_CURRENT_SOURCE_DIR}/files/websockify.service DESTINATION ${CONFIG_INSTALL_DIR}/systemd/system)
        install(FILES ${CMAKE_CURRENT_SOURCE_DIR}/files/astroberry-manager.service DESTINATION ${CONFIG_INSTALL_DIR}/systemd/system)
        install(FILES ${CMAKE_CURRENT_SOURCE_DIR}/files/astroberry.service DESTINATION ${CONFIG_INSTALL_DIR}/avahi/services)
	install(FILES ${CMAKE_CURRENT_SOURCE_DIR}/files/smb.conf DESTINATION ${CONFIG_INSTALL_DIR}/samba)
        install(FILES ${CMAKE_CURRENT_SOURCE_DIR}/files/Hotspot.nmconnection DESTINATION ${CONFIG_INSTALL_DIR}/NetworkManager/system-connections PERMISSIONS OWNER_READ OWNER_WRITE)

        install(FILES ${CMAKE_CURRENT_SOURCE_DIR}/files/lightdm-gtk-greeter.conf DESTINATION ${CONFIG_INSTALL_DIR}/lightdm/lightdm-gtk-greeter.conf)
        install(FILES ${CMAKE_CURRENT_SOURCE_DIR}/files/xfce4-session.xml DESTINATION ${CONFIG_INSTALL_DIR}/xdg/xfce4/xfconf/xfce-perchannel-xml/xfce4-session.xml)
        install(FILES ${CMAKE_CURRENT_SOURCE_DIR}/files/xsettings.xml DESTINATION ${CONFIG_INSTALL_DIR}/xdg/xfce4/xfconf/xfce-perchannel-xml/xsettings.xml)
        install(FILES ${CMAKE_CURRENT_SOURCE_DIR}/files/default.xml DESTINATION ${CONFIG_INSTALL_DIR}/xdg/xfce4/panel/default.xml)
        install(FILES ${CMAKE_CURRENT_SOURCE_DIR}/files/xfce-applications.menu DESTINATION ${CONFIG_INSTALL_DIR}/xdg/menus)

        install(FILES ${CMAKE_CURRENT_SOURCE_DIR}/files/meta-data DESTINATION ${BOOT_INSTALL_DIR}/firmware)
        install(FILES ${CMAKE_CURRENT_SOURCE_DIR}/files/user-data DESTINATION ${BOOT_INSTALL_DIR}/firmware)
        install(FILES ${CMAKE_CURRENT_SOURCE_DIR}/files/network-config DESTINATION ${BOOT_INSTALL_DIR}/firmware)

        install(FILES ${CMAKE_CURRENT_SOURCE_DIR}/files/astroberry-os-init DESTINATION ${BIN_INSTALL_DIR})
        install(FILES ${CMAKE_CURRENT_SOURCE_DIR}/files/astroberry-desktop-init DESTINATION ${BIN_INSTALL_DIR})

	install(FILES ${CMAKE_CURRENT_BINARY_DIR}/version DESTINATION ${CONFIG_INSTALL_DIR}/astroberry)
endif()
