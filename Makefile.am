AUTOMAKE_OPTIONS = foreign
SUBDIRS = doc

LLIBDIR=@LIBDIR@ 
lib_LTLIBRARIES = libg15.la
libg15_la_SOURCES = libg15.h libg15.c
libg15_la_LDFLAGS = -version-info 1:1:0
include_HEADERS= libg15.h
EXTRA_DIST = 
ACLOCAL_AMFLAGS = -I m4

pkgconfigdir=$(libdir)/pkgconfig
pkgconfig_DATA=libg15.pc

