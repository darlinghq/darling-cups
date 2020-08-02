project(cups-systemv)

foreach(EXE IN ITEMS cancel cupsaccept cupsctl cupstestppd lp lpadmin lpinfo lpmove lpoptions lpstat)
	add_darling_executable(${EXE}
		${EXE}.c
	)
	target_link_libraries(${EXE}
		cups
	)
endforeach()

install(
	TARGETS
		cupsaccept
		cupsctl
		lpadmin
		lpinfo
		lpmove
	DESTINATION libexec/darling/usr/sbin
)

install(
	TARGETS
		cancel
		cupstestppd
		lp
		lpoptions
		lpstat
	DESTINATION libexec/darling/usr/bin
)

foreach(LINK IN ITEMS cupsdisable cupsenable cupsreject)
	InstallSymlink("cupsaccept" "${CMAKE_INSTALL_PREFIX}/libexec/darling/usr/bin/${LINK}")
endforeach()
