project(cups-conf)

# variable from the Makefile
#
# we reuse this because we need to install these files
# as both their normal names and also their names with ".default" appended
# (and CMake only allows you to rename if you're installing a single file at a time)
set(KEEP cups-files.conf cupsd.conf snmp.conf)

foreach(ITEM IN LISTS KEEP)
	install(FILES ${ITEM} DESTINATION libexec/darling/private/etc/cups)
	install(FILES ${ITEM} DESTINATION libexec/darling/private/etc/cups RENAME ${ITEM}.default)
endforeach()

install(
	FILES
		mime.convs
		mime.types
	DESTINATION libexec/darling/usr/share/cups/mime
)
