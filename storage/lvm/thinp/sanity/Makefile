# The name of the package under test
PACKAGE_NAME=kernel

# The toplevel namespace within which the test lives.
TOPLEVEL_NAMESPACE=/$(PACKAGE_NAME)

# The version of the test rpm that gets
#  created / submitte
export TESTVERSION=1.0

# The path of the test below the package
RELATIVE_PATH=storage/lvm/thinp/sanity

# The relative path name to the test 
export TEST=$(TOPLEVEL_NAMESPACE)/$(RELATIVE_PATH)

# Name of the tar file that will be bundled in the rpm
TARGET=iozone3_414

FILES=	$(METADATA)      \
	runtest.sh       \
	Makefile

clean:
	$(RM) *~ rm $(METADATA)
	rm -rf $(TARGET) rh-tests-kernel-*.rpm
	rm -rf $(TARGET).tar
	rm -f iozone *.txt

run: build
	chmod +x ./runtest.sh
	./runtest.sh

build: $(METADATA) $(TARGET)
	make -C iozone3_414/src/current/ linux
	cp -f iozone3_414/src/current/iozone ./

$(TARGET).tar:
	wget http://www.iozone.org/src/current/$(TARGET).tar

$(TARGET): $(TARGET).tar
	tar -xvf $(TARGET).tar

# Include a global make rules file
include /usr/share/rhts/lib/rhts-make.include

showmeta: $(METADATA)
	@cat $(METADATA)
	@rhts-lint $(METADATA)

$(METADATA):
	touch $(METADATA)
	@echo "Name:		$(TEST)"	> $(METADATA)
	@echo "Description:	Sanity test for lvm thinp" >> $(METADATA)
	@echo "Path:		$(TEST_DIR)"	>> $(METADATA)
	@echo "TestTime:	60m"		>> $(METADATA)
	@echo "TestVersion:	$(TESTVERSION)"	>> $(METADATA)
	@echo "Releases:	RedHatEnterpriseLinux7 RedHatEnterpriseLinuxPegas7 RedHatEnterpriseLinuxAlternateArchitectures7 Fedora25 Fedora26 Fedorarawhide" >> $(METADATA)
	@echo "#Architectures:	All"		>> $(METADATA)
	@echo "Destructive:	no"		>> $(METADATA)
	@echo "Type:            KernelTier0 KernelTier1"    >> $(METADATA)
	@echo "Priority:	Normal"		>> $(METADATA)
	@echo "RunFor:		kernel"		>> $(METADATA)
	@echo "Requires:	kernel-devel"	>> $(METADATA)
	@echo "Requires:	lvm2"           >> $(METADATA)
	@echo "Requires:	gcc"            >> $(METADATA)
	@echo "Requires:	make"           >> $(METADATA)
	@echo "Requires:	glibc-static"   >> $(METADATA)
	@echo "Requires:	gnuplot"	>> $(METADATA)
	@echo "Owner:		Jakub Krysl <jkrysl@redhat.com>" >> $(METADATA)
	@echo "License:		GPLv2"		>> $(METADATA)
