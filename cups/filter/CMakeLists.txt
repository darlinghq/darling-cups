project(cups-filter)

# pstops is special
# it gets *two* source files *gasp*
add_darling_executable(pstops
	common.c
	pstops.c
)
target_link_libraries(pstops
	cups
)
install(TARGETS pstops DESTINATION libexec/darling/usr/libexec/cups/filter)

foreach(EXE IN ITEMS commandtops gziptoany rastertoepson rastertohp rastertolabel rastertopwg)
	add_darling_executable(${EXE}
		${EXE}.c
	)
	target_link_libraries(${EXE}
		cups
	)
	install(TARGETS ${EXE} DESTINATION libexec/darling/usr/libexec/cups/filter)
endforeach()
