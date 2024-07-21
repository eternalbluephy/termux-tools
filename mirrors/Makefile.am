# Default mirrors
pkgdata_MIRRORS = default

install-default: $(pkgdata_MIRRORS)
	$(MKDIR_P) $(DESTDIR)$(sysconfdir)/termux/mirrors
	for f in $(pkgdata_MIRRORS); do \
		$(INSTALL) -m 644 $(srcdir)/$$f \
		$(DESTDIR)$(sysconfdir)/termux/mirrors; \
	done

uninstall-default:
	for f in $(pkgdata_MIRRORS); do \
		rm -f $(DESTDIR)$(sysconfdir)/termux/mirrors/$$f; \
	done
	-rmdir $(DESTDIR)$(sysconfdir)/termux/mirrors



uninstall-removed-mirrors:
	for f in $(pkgdata_MIRRORS_REMOVED); do \
		rm -f $(DESTDIR)$(sysconfdir)/termux/mirrors/$$f; \
	done



create-deb-control-files:
	sh -c "cd $$(dirname $(DESTDIR)$(sysconfdir)); find $$(basename $(DESTDIR)$(sysconfdir))/termux/mirrors -type f" >> ../conffiles;
	printf "# Delete removed mirrors\nfor f in %s; do\n    if test -f \"%s/etc/termux/mirrors/\$$f\"; then\n        echo \"Deleting removed mirror: \$$f\"; rm -f \"%s/etc/termux/mirrors/\$$f\";\n    fi\ndone" "$(pkgdata_MIRRORS_REMOVED)" "$(termux_prefix)" "$(termux_prefix)" >> ../preinst;



install-data-local: uninstall-removed-mirrors install-default

uninstall-local: uninstall-removed-mirrors uninstall-default

EXTRA_DIST = $(pkgdata_MIRRORS)
