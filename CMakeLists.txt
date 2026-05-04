cmake_minimum_required(VERSION 2.8)
PROJECT(astroberry-os-sysmod NONE)

set (VERSION_MAJOR 3)
set (VERSION_MINOR 2)
set (VERSION_RELEASE 0)

set(CONFIG_INSTALL_DIR "/etc")
set(BOOT_INSTALL_DIR "/boot")
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
	# Add system services
	install(FILES ${CMAKE_CURRENT_SOURCE_DIR}/files/services/vncserver.service DESTINATION ${CONFIG_INSTALL_DIR}/systemd/system)
	install(FILES ${CMAKE_CURRENT_SOURCE_DIR}/files/services/indiwebmanager.service DESTINATION ${CONFIG_INSTALL_DIR}/systemd/system)
	install(FILES ${CMAKE_CURRENT_SOURCE_DIR}/files/services/websockify.service DESTINATION ${CONFIG_INSTALL_DIR}/systemd/system)
        install(FILES ${CMAKE_CURRENT_SOURCE_DIR}/files/services/astroberry-manager.service DESTINATION ${CONFIG_INSTALL_DIR}/systemd/system)
        install(FILES ${CMAKE_CURRENT_SOURCE_DIR}/files/services/astroberry.service DESTINATION ${CONFIG_INSTALL_DIR}/avahi/services)
	# Add hotspot
        install(FILES ${CMAKE_CURRENT_SOURCE_DIR}/files/hotspot/Hotspot.nmconnection DESTINATION ${CONFIG_INSTALL_DIR}/NetworkManager/system-connections PERMISSIONS OWNER_READ OWNER_WRITE)
	# Add first boot init scripts
        install(FILES ${CMAKE_CURRENT_SOURCE_DIR}/files/firstboot/astroberry-os-init DESTINATION ${BIN_INSTALL_DIR})
        install(FILES ${CMAKE_CURRENT_SOURCE_DIR}/files/firstboot/astroberry-desktop-init DESTINATION ${BIN_INSTALL_DIR})
	# Add Astroberry OS version file
	install(FILES ${CMAKE_CURRENT_BINARY_DIR}/version DESTINATION ${CONFIG_INSTALL_DIR}/astroberry)
endif()
