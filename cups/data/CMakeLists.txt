project(cups-data)

install(
	FILES
		epson.h
		font.defs
		hp.h
		label.h
		media.defs
		raster.defs
	DESTINATION libexec/darling/usr/share/cups/ppdc
)

# install empty directories
foreach(DIR IN ITEMS banners data model profiles)
	install(DIRECTORY DESTINATION libexec/darling/usr/share/cups/${DIR})
endforeach()
