project(cups-man)

set(man1
	cancel.1
	cups.1
	cups-config.1
	cupstestppd.1
	ippeveprinter.1
	ippfind.1
	ipptool.1
	lp.1
	lpoptions.1
	lpq.1
	lprm.1
	lpr.1
	lpstat.1
	ppdc.1
	ppdhtml.1
	ppdi.1
	ppdmerge.1
	ppdpo.1
)

set(man5
	classes.conf.5
	client.conf.5
	cups-files.conf.5
	cups-snmp.conf.5
	cupsd.conf.5
	cupsd-logs.5
	ipptoolfile.5
	mailto.conf.5
	mime.convs.5
	mime.types.5
	ppdcfile.5
	printers.conf.5
	subscriptions.conf.5
)

set(man7
	backend.7
	filter.7
	ippevepcl.7
	notifier.7
)

set(man8
	cupsaccept.8
	cupsctl.8
	cupsfilter.8
	cups-lpd.8
	cups-snmp.8
	cupsd.8
	cupsd-helper.8
	cupsenable.8
	lpadmin.8
	lpinfo.8
	lpmove.8
	lpc.8
)

install(FILES ${man1} DESTINATION libexec/darling/usr/share/man/man1)
install(FILES ${man5} DESTINATION libexec/darling/usr/share/man/man5)
install(FILES ${man7} DESTINATION libexec/darling/usr/share/man/man7)
install(FILES ${man8} DESTINATION libexec/darling/usr/share/man/man8)

InstallSymlink("ippevepcl.7" "${CMAKE_INSTALL_PREFIX}/libexec/darling/usr/share/man/man7/ippeveps.7")
InstallSymlink("cupsenable.8" "${CMAKE_INSTALL_PREFIX}/libexec/darling/usr/share/man/man8/cupsdisable.8")
InstallSymlink("cupsaccept.8" "${CMAKE_INSTALL_PREFIX}/libexec/darling/usr/share/man/man8/cupsreject.8")

foreach(LINK IN ITEMS cups-deviced.8 cups-driverd.8 cups-exec.8)
	InstallSymlink("cupsd-helper.8" "${CMAKE_INSTALL_PREFIX}/libexec/darling/usr/share/man/man8/${LINK}")
endforeach()
