project(cups-ppdc)

add_darling_static_library(cups_ppdc FAT SOURCES
	ppdc-array.cxx
	ppdc-attr.cxx
	ppdc-catalog.cxx
	ppdc-choice.cxx
	ppdc-constraint.cxx
	ppdc-driver.cxx
	ppdc-file.cxx
	ppdc-filter.cxx
	ppdc-font.cxx
	ppdc-group.cxx
	ppdc-import.cxx
	ppdc-mediasize.cxx
	ppdc-message.cxx
	ppdc-option.cxx
	ppdc-profile.cxx
	ppdc-shared.cxx
	ppdc-source.cxx
	ppdc-string.cxx
	ppdc-variable.cxx
)

foreach(EXE IN ITEMS ppdc ppdhtml ppdi ppdmerge ppdpo)
	add_darling_executable(${EXE}
		${EXE}.cxx
	)
	target_link_libraries(${EXE}
		cups
		cups_ppdc

		cxx
	)
	install(TARGETS ${EXE} DESTINATION libexec/darling/usr/bin)
endforeach()

install(FILES sample.drv DESTINATION libexec/darling/usr/share/cups/drv)
