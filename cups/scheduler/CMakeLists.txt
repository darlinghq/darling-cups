project(cups-scheduler)

add_darling_static_library(cups_mime FAT SOURCES
	filter.c
	mime.c
	type.c
)

add_darling_object_library(cups_scheduler_util
	util.c
)

add_darling_executable(cupsd
	auth.c
	banners.c
	cert.c
	classes.c
	client.c
	colorman.c
	conf.c
	dirsvc.c
	env.c
	file.c
	main.c
	ipp.c
	listen.c
	job.c
	log.c
	network.c
	policy.c
	printers.c
	process.c
	quotas.c
	select.c
	server.c
	statbuf.c
	subscriptions.c
	sysman.c
)
target_link_libraries(cupsd
	cups_mime

	pam.2
	IOKit
	ApplicationServices
	Kerberos
	GSS
	resolv-darwin
	SystemConfiguration
	CoreFoundation
	Security
	iconv
	z
)

add_darling_executable(cupsfilter
	cupsfilter.c
)
target_link_libraries(cupsfilter
	cups_mime
)

add_darling_executable(cups-deviced
	cups-deviced.c
	$<TARGET_OBJECTS:cups_scheduler_util>
)

add_darling_executable(cups-driverd
	cups-driverd.cxx
	$<TARGET_OBJECTS:cups_scheduler_util>
)
target_link_libraries(cups-driverd
	cups_ppdc

	resolv-darwin
	SystemConfiguration
	CoreFoundation
	Security
	iconv
	z

	cxx
)

add_darling_executable(cups-exec
	cups-exec.c
)

add_darling_executable(cups-lpd
	cups-lpd.c
)

#
# link everything with libcups
#
foreach(EXE IN ITEMS cupsd cupsfilter cups-deviced cups-driverd cups-exec cups-lpd)
	target_link_libraries(${EXE}
		cups
	)
endforeach()

#
# install everything
#

install(
	TARGETS
		cupsd
		cupsfilter
	DESTINATION libexec/darling/usr/sbin
)

install(
	TARGETS
		cups-deviced
		cups-driverd
		cups-exec
		cups-lpd
	DESTINATION libexec/darling/usr/libexec/cups/daemon
)

install(
	FILES
		org.cups.cupsd.plist
		org.cups.cups-lpd.plist
	DESTINATION libexec/darling/System/Library/LaunchDaemons
)

set(EMPTY_DIRS
	usr/libexec/cups/driver
	private/etc/cups/ppd
	private/etc/cups/certs
	private/var/log/cups
	private/var/spool/cups/tmp
	private/var/spool/cups/cache
)

foreach(EMPTY_DIR IN LISTS EMPTY_DIRS)
	install(DIRECTORY DESTINATION libexec/darling/${EMPTY_DIR})
endforeach()

