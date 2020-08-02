project(cups-backend)

add_darling_static_library(cups_libbackend FAT SOURCES
	ieee1284.c
	network.c
	runloop.c
	snmp-supplies.c
)

#
# link everything with libcups and libbackend
#
foreach(EXE IN ITEMS ipp lpd dnssd snmp socket usb)
	add_darling_executable(${EXE}
		${EXE}.c
	)
	target_link_libraries(${EXE}
		cups
		cups_libbackend
	)
endforeach()

# `usb` requires some additional libraries
target_link_libraries(usb
	IOKit
	resolv-darwin
	SystemConfiguration
	CoreFoundation
	Security
	iconv
	z
)

#
# install everything
#

# XPC stuff
install(TARGETS ipp DESTINATION darling/libexec/usr/libexec/cups/apple)
foreach(LINK IN ITEMS http https ipps)
	InstallSymlink("ipp" "${CMAKE_INSTALL_PREFIX}/darling/libexec/usr/libexec/cups/apple/${LINK}")
endforeach()

# root backends
install(
	TARGETS
		ipp
		lpd
		dnssd
	PERMISSIONS
		OWNER_READ OWNER_WRITE OWNER_EXECUTE
	DESTINATION darling/libexec/usr/libexec/cups/backend
)

# user backends
install(
	TARGETS
		snmp
		socket
	DESTINATION darling/libexec/usr/libexec/cups/backend
)

foreach(LINK IN ITEMS http https ipps)
	InstallSymlink("ipp" "${CMAKE_INSTALL_PREFIX}/darling/libexec/usr/libexec/cups/backend/${LINK}")
endforeach()

InstallSymlink("dnssd" "${CMAKE_INSTALL_PREFIX}/darling/libexec/usr/libexec/cups/backend/mdns")

install(TARGETS usb DESTINATION darling/libexec/usr/libexec/cups/backend)
