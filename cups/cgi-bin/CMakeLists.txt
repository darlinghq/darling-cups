project(cups-cgi-bin)

add_darling_static_library(cups_cgi FAT SOURCES
	help-index.c
	html.c
	ipp-var.c
	search.c
	template.c
	var.c
)

foreach(CGI IN ITEMS admin classes help jobs printers)
	add_darling_executable(${CGI}.cgi
		${CGI}.c
	)
	target_link_libraries(${CGI}.cgi
		cups
		cups_cgi
	)
	install(TARGETS ${CGI}.cgi DESTINATION libexec/darling/usr/libexec/cups/cgi-bin)
endforeach()
