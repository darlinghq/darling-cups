project(cups)

add_compile_definitions(
	_CUPS_SOURCE
	_FORTIFY_SOURCE=2
	_LARGEFILE_SOURCE
	_LARGEFILE64_SOURCE
	_THREAD_SAFE
	_REENTRANT
)

add_compile_options(
	-w
)

add_link_options(
	-Wl,-pie
)

include_directories(
	${CMAKE_CURRENT_SOURCE_DIR}/cups
	${CMAKE_CURRENT_SOURCE_DIR}/cups/xcode
)

add_subdirectory(cups/cups)
add_subdirectory(cups/tools)
add_subdirectory(cups/filter)
add_subdirectory(cups/backend)
add_subdirectory(cups/berkeley)
add_subdirectory(cups/cgi-bin)
add_subdirectory(cups/monitor)
add_subdirectory(cups/notifier)
add_subdirectory(cups/ppdc)
add_subdirectory(cups/scheduler)
add_subdirectory(cups/systemv)
add_subdirectory(cups/conf)
add_subdirectory(cups/data)
add_subdirectory(cups/locale)
add_subdirectory(cups/man)
add_subdirectory(cups/templates)
# TODO: install docs (i.e. the "doc" directory)
