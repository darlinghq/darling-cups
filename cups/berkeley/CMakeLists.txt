project(cups-berkeley)

foreach(EXE IN ITEMS lpc lpq lpr lprm)
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
		lpq
		lpr
		lprm
	DESTINATION libexec/darling/usr/bin
)

install(TARGETS lpc DESTINATION libexec/darling/usr/sbin)
