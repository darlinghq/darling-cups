project(cups-tools)

#
# link everything with libcups
#

foreach(EXE IN ITEMS ippevepcl ippeveps ippeveprinter ippfind ipptool)
	add_darling_executable(${EXE}
		${EXE}.c
	)
	target_link_libraries(${EXE}
		cups
	)
endforeach()

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
