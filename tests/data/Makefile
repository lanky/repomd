RPMS := $(addsuffix .rpm,brisket chicken ribs sausage)
TOPDIR := $(shell pwd)/rpmbuild
DIST := .fc27

all: repo empty_repo

%.rpm:
	@mkdir $(TOPDIR)
	@rpmbuild --define "_topdir $(TOPDIR)" --define "dist $(DIST)" --define "vendor Carl's BBQ" --define "packager Carl" -bb $(basename $@).spec
	@mv $(TOPDIR)/RPMS/noarch/*.rpm .
	@[ -d $(TOPDIR) ] && rm -r $(TOPDIR)

repo: $(RPMS)
	@mkdir repo
	@mv *.rpm repo
	@createrepo_c --simple-md-filenames --no-database --outputdir repo repo
	@rm repo/repodata/filelists.xml.gz repo/repodata/other.xml.gz repo/*.rpm

empty_repo:
	@mkdir empty_repo
	@createrepo_c --simple-md-filenames --no-database --outputdir empty_repo empty_repo
	@rm empty_repo/repodata/filelists.xml.gz empty_repo/repodata/other.xml.gz

clean:
	@if test -d repo; then rm -r repo; fi
	@if test -d empty_repo; then rm -r empty_repo; fi
