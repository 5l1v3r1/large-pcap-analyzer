## Process this file with automake to produce Makefile.in

# avoid warnings about this packet not being in GNU style:
AUTOMAKE_OPTIONS = foreign subdir-objects
ACLOCAL_AMFLAGS = -I m4

bin_PROGRAMS = large_pcap_analyzer
large_pcap_analyzer_SOURCES = src/large-pcap-analyzer.cpp src/filter.cpp src/parse.cpp src/processor.cpp src/pcap_helpers.cpp

check: $(bin_PROGRAMS)
	cd test-pcaps && chmod a+x ./run_tests.sh && bash run_tests.sh

# "test" or "tests" are just synonyms of "check"
test: check
tests: check

distclean:
	rm -f Makefile config.log config.status src/.dirstamp src/config.h src/stamp-h1
	rm -rf autom4te.cache snap/.snapcraft src/.deps


#
# REMINDERS TO MYSELF FOR RELEASING A NEW VERSION:
#
# Ubuntu snap release process:
# ----------------------------
# The simpler release process uses Snapcraft/Github integration and requires:
# 1) create a new release tarball in Github so that the URL:
#      https://github.com/f18m/large-pcap-analyzer/archive/NEW_VERSION.tar.gz
#    becomes available
# 2) log into Snapcraft at https://build.snapcraft.io/user/f18m/large-pcap-analyzer
#    and hit the "Build manually now" button.
#
# COPR release process:
# ----------------------------
# 1) log into https://copr.fedorainfracloud.org/coprs/f18m/large-pcap-analyzer/builds/
# 2) hit the new 


#  this is the MANUAL way to upload a new SNAP but it will be uploaded only for amd64 architecture!
release_new_version:
	snap remove large-pcap-analyzer                                 # in case it was already installed
	snapcraft                                                       # this will rebuild the snap using snap/snapcraft.yaml
	snap install large-pcap-analyzer_*_amd64.snap --devmode         # test new snap installation
	snap list                                                       # confirm new version is now installed
	snapcraft login                                                 # this is interactive and will ask email & password
	snapcraft push --release=stable large-pcap-analyzer_*_amd64.snap   # release upstream
