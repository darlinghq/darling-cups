project(cups-monitor)

foreach(EXE IN ITEMS bcp tbcp)
	add_darling_executable(${EXE}
		${EXE}.c
	)
	target_link_libraries(${EXE}
		cups
	)
	install(TARGETS ${EXE} DESTINATION libexec/darling/usr/libexec/cups/monitor)
endforeach()
