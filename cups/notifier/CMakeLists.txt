project(cups-notifier)

foreach(EXE IN ITEMS mailto rss)
	add_darling_executable(${EXE}
		${EXE}.c
	)
	target_link_libraries(${EXE}
		cups
	)
	install(TARGETS ${EXE} DESTINATION libexec/darling/usr/libexec/cups/notifier)
endforeach()

# install an empty directory
install(DIRECTORY DESTINATION libexec/darling/private/var/spool/cups/cache/rss)
