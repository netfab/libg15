SHELL = /bin/sh
top_srcdir = ..
build_dir= ../build
PREFIX_DEV_DIR=/var/tmp/devcxx
PREFIX_DIR=$(PREFIX_DEV_DIR)/libg15
LANG=C
CFLAGS="-march=sandybridge -mtune=generic -O2 -pipe -mmmx -msse -msse2"
CONFIG_AUX_DIR=config
CONFIG_MACRO_DIR=m4

MAINTAINERCLEANFILES = \
    $(CONFIG_AUX_DIR)/compile \
	$(CONFIG_AUX_DIR)/config.guess \
	$(CONFIG_AUX_DIR)/config.sub \
	$(CONFIG_AUX_DIR)/depcomp \
	$(CONFIG_AUX_DIR)/install-sh \
	$(CONFIG_AUX_DIR)/ltmain.sh \
	$(CONFIG_AUX_DIR)/missing \
	$(CONFIG_MACRO_DIR)/libtool.m4 \
	$(CONFIG_MACRO_DIR)/ltoptions.m4 \
	$(CONFIG_MACRO_DIR)/ltsugar.m4 \
	$(CONFIG_MACRO_DIR)/ltversion.m4 \
	$(CONFIG_MACRO_DIR)/lt~obsolete.m4 \
	aclocal.m4 \
    config.h.in \
    configure

all:
	@echo "Available targets :"
	@echo " autoreconf_it configure_it build_it install_it distcheck_it"
	@echo " uninstall_it clean_it fullclean_it init_dir all"
	@echo

init_dir:
	test ! -d $(build_dir) && mkdir -p $(build_dir) || echo "build_dir already present"

autoreconf_it:
	cd $(top_srcdir) && autoreconf -i


configure_it: init_dir
	cd $(build_dir) && $(top_srcdir)/configure CFLAGS=$(CFLAGS) \
	--srcdir=$(top_srcdir) --prefix=$(PREFIX_DIR)

build_it:
	cd $(build_dir) && make

install_it:
	cd $(build_dir) && make install

uninstall_it:
	cd $(build_dir) && test -d "$(PREFIX_DIR)" && make uninstall || echo 'no need uninstall phase.'
	cd "$(PREFIX_DEV_DIR)" && rmdir -v libg15/lib || echo 'uninstall artefacts rmdir failure 1.'
	cd "$(PREFIX_DEV_DIR)" && rmdir -v -p libg15/include || echo 'uninstall artefacts rmdir failure 2.'

clean_it: uninstall_it
	cd $(build_dir) && make clean

fullclean_it: clean_it
	cd $(build_dir) && make maintainer-clean
	cd $(top_srcdir) && rm -v $(MAINTAINERCLEANFILES)
	find $(top_srcdir) -name 'Makefile.in' -delete
	cd $(build_dir) && find . -depth -type d -delete
	cd $(build_dir) && test -f *.tar.gz && rm -v *.tar.gz || echo 'archive not found.'
	rmdir -v $(build_dir)
	rmdir -v ../$(CONFIG_AUX_DIR)

distcheck_it:
	cd $(build_dir) && make distcheck

