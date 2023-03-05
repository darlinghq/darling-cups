project(cups-tools)

#
# link everything with libcups
#

foreach(EXE IN ITEMS ippevepcl ippeveps ippfind ipptool)
	add_darling_executable(${EXE}
		${EXE}.c
	)
	target_link_libraries(${EXE}
		cups
	)
endforeach()

add_darling_executable(ippeveprinter
	ippeveprinter.c
)

target_link_libraries(ippeveprinter
	cups
	pam.2
)

#
# install everything
#

install(
	TARGETS
		ippeveprinter
		ippfind
		ipptool
	DESTINATION libexec/darling/usr/bin
)

install(
	TARGETS
		ippevepcl
		ippeveps
	DESTINATION libexec/darling/usr/libexec/cups/command
)
