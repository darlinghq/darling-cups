project(cups-core)

#
# libcups
#

set(DYLIB_INSTALL_NAME "/usr/lib/libcups.2.dylib")
set(DYLIB_COMPAT_VERSION "2.0.0")
set(DYLIB_CURRENT_VERSION "2.14.0")

add_darling_library(cups
	# core
	array.c
	auth.c
	debug.c
	dest.c
	dest-job.c
	dest-localization.c
	dest-options.c
	dir.c
	encode.c
	file.c
	getputfile.c
	globals.c
	hash.c
	http.c
	http-addr.c
	http-addrlist.c
	http-support.c
	ipp.c
	ipp-file.c
	ipp-vars.c
	ipp-support.c
	langprintf.c
	language.c
	md5.c
	md5passwd.c
	notify.c
	options.c
	pwg-media.c
	raster-error.c
	raster-stream.c
	raster-stubs.c
	request.c
	snprintf.c
	string.c
	tempfile.c
	thread.c
	tls.c
	transcode.c
	usersys.c
	util.c

	# drivers
	adminutil.c
	backchannel.c
	backend.c
	getdevices.c
	getifaddrs.c
	ppd.c
	ppd-attr.c
	ppd-cache.c
	ppd-conflicts.c
	ppd-custom.c
	ppd-emit.c
	ppd-localize.c
	ppd-mark.c
	ppd-page.c
	ppd-util.c
	raster-interpret.c
	raster-interstub.c
	sidechannel.c
	snmp.c
)
target_link_libraries(cups
	Kerberos
	GSS
	resolv-darwin
	SystemConfiguration
	CoreFoundation
	Security
	iconv
	z
	system
)
set_target_properties(cups PROPERTIES OUTPUT_NAME "cups.2")

#
# libcupsimage
#

set(DYLIB_INSTALL_NAME "/usr/lib/libcupsimage.2.dylib")
set(DYLIB_COMPAT_VERSION "2.0.0")
set(DYLIB_CURRENT_VERSION "2.3.0")

add_darling_library(cupsimage
	raster-interstub.c
	raster-stubs.c
)
target_link_libraries(cupsimage
	cups
	system
)
set_target_properties(cups PROPERTIES OUTPUT_NAME "cupsimage.2")

#
# install everything
#

install(
	TARGETS
		cups
		cupsimage
	DESTINATION libexec/darling/usr/lib
)

InstallSymlink("libcups.2.dylib" "${CMAKE_INSTALL_PREFIX}/libexec/darling/usr/lib/libcups.dylib")
InstallSymlink("libcupsimage.2.dylib" "${CMAKE_INSTALL_PREFIX}/libexec/darling/usr/lib/libcupsimage.dylib")
