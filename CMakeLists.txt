project(cups)

add_definitions(
	-w
	-D_CUPS_SOURCE
	-D_LARGEFILE_SOURCE
	-D_LARGEFILE64_SOURCE
	-D_THREAD_SAFE
	-D_REENTRANT
	-iquote "${CMAKE_CURRENT_SOURCE_DIR}/cups"
)

include_directories(${CMAKE_CURRENT_SOURCE_DIR}/cups)

set(DYLIB_INSTALL_NAME "/usr/lib/libcups.2.dylib")
set(DYLIB_COMPAT_VERSION "2.0.0")
set(DYLIB_CURRENT_VERSION "2.14.0")

add_darling_library(cups
	cups/cups/array.c
	cups/cups/auth.c
	cups/cups/debug.c
	cups/cups/dest.c
	cups/cups/dest-job.c
	cups/cups/dest-localization.c
	cups/cups/dest-options.c
	cups/cups/dir.c
	cups/cups/encode.c
	cups/cups/file.c
	cups/cups/getputfile.c
	cups/cups/globals.c
	cups/cups/hash.c
	cups/cups/http.c
	cups/cups/http-addr.c
	cups/cups/http-addrlist.c
	cups/cups/http-support.c
	cups/cups/ipp.c
	cups/cups/ipp-file.c
	cups/cups/ipp-vars.c
	cups/cups/ipp-support.c
	cups/cups/langprintf.c
	cups/cups/language.c
	cups/cups/md5.c
	cups/cups/md5passwd.c
	cups/cups/notify.c
	cups/cups/options.c
	cups/cups/pwg-media.c
	cups/cups/raster-error.c
	cups/cups/raster-stream.c
	cups/cups/raster-stubs.c
	cups/cups/request.c
	cups/cups/snprintf.c
	cups/cups/string.c
	cups/cups/tempfile.c
	cups/cups/thread.c
	cups/cups/tls.c
	cups/cups/transcode.c
	cups/cups/usersys.c
	cups/cups/util.c
)
target_link_libraries(cups resolv-darwin SystemConfiguration CoreFoundation Security iconv z)
set_target_properties(cups PROPERTIES OUTPUT_NAME "cups.2")
install(TARGETS cups DESTINATION libexec/darling/usr/lib)
InstallSymlink("libcups.2.dylib" "${CMAKE_INSTALL_PREFIX}/libexec/darling/usr/lib/libcups.dylib")
