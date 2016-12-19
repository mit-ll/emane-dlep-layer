XML=                        \
 emanedleplayer.xml

EXTRA_DIST=                 \
 emanedleplayer.xml.in

edit = sed                  \
 -e 's|@datadir[@]|$(pkgdatadir)|g'  

all-local:	$(XML)

emanedleplayer.xml:	emanedleplayer.xml.in
	$(edit) $< > $@

clean-local:
	-rm -f $(XML)

install-exec-hook:
	$(mkinstalldirs) $(DESTDIR)$(datadir)/$(PACKAGE)/xml
	-cp -f $(XML)  $(DESTDIR)$(datadir)/$(PACKAGE)/xml

uninstall-local:
	rm -f  $(DESTDIR)$(datadir)/$(PACKAGE)/xml/*

