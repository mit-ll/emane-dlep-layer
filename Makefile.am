ACLOCAL_AMFLAGS = -I m4

SUBDIRS=                     \
 include                     \
 src                         \
 src/xml

cleantar:
	@(rm -f emanedleplayer*.tar.gz)

edit = sed \
       -e 's|@VERSION[@]|$(VERSION)|g'

clean-local: cleantar cleandeb
	-rm -rf .rpmbuild
	-rm -rf .debbuild
	-rm -f emanedleplayer.spec
	-rm -f debian/changelog


EXTRA_DIST =            \
 AUTHORS                \
 COPYING                \
 ChangeLog              \
 NEWS                   \
 emanedleplayer.spec.in \
 SPONSOR                \
 debian


if HAVE_DEB
deb: clean-local dist-gzip
	mkdir -p .debbuild
	cp -f $(PACKAGE)-$(VERSION).tar.gz .debbuild
	cd .debbuild && tar xzf $(PACKAGE)-$(VERSION).tar.gz
	$(edit) .debbuild/$(PACKAGE)-$(VERSION)/debian/changelog.in > \
	.debbuild/$(PACKAGE)-$(VERSION)/debian/changelog
	cd .debbuild/$(PACKAGE)-$(VERSION) && dpkg-buildpackage -F -us -uc
	@echo "============================================================"
	@echo "debs located in .debbuild"
cleandeb:
	dh_clean
else
cleandeb:
endif



if HAVE_RPMBUILD
rpm:    clean-local dist-gzip
	$(edit) emanedleplayer.spec.in > emanedleplayer.spec
	mkdir -p .rpmbuild/BUILD \
	.rpmbuild/SPECS \
	.rpmbuild/SOURCES \
	.rpmbuild/SRPMS \
	.rpmbuild/RPMS/$(RPMARCH) \
	.rpmbuild/tmp
	cp -f $(PACKAGE)-$(VERSION).tar.gz .rpmbuild/SOURCES
	rpmbuild --clean -bb $(top_srcdir)/emanedleplayer.spec --define "_topdir $$PWD/.rpmbuild" --define "_tmppath $$PWD/.rpmbuild/tmp"
	@echo "============================================================"
	@echo "RPMs located in .rpmbuild/RPMS and .rpmbuild/SRPMS"
endif


DISTCLEANFILES = debian/changelog
