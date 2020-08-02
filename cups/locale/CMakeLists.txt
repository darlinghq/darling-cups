project(cups-locale)

install(
	FILES cups.strings
	DESTINATION "libexec/darling/System/Library/Frameworks/ApplicationServices.framework/Versions/A/Frameworks/PrintCore.framework/Versions/A/Resources/en.lproj"
)
