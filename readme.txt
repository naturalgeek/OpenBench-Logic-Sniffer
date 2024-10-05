# Updating Firmware in 2024

I've had some troubles updating the firmware, blogs refered to a not anymore existing file:
https://github.com/downloads/GadgetFactory/OpenBench-Logic-Sniffer/ols-0308-expert.tgz

There seems to be "no copy" of this archive in the interweb and the source repo lacks of important binaries which become more and more difficult to compile from source due to legacy of dependencies.

Luckily there is a fork of the origin repo which still contains some recent binaries and this repo here is a for of if to keep it "safe"

I successfully updated my device on a Ubuntu Jammy in late 2024. hooray!

Steps to do so:

- Checkout this code
- cd OLS_Upgrade/linbin
- ./ols-loader
-> this will throw a missing libusb error. This is because you probably run a 64bit system. so install the x86 version of that library
- sudo apt-get install libusb-0.1-4:i386

Now you can flash the Demon-Core
- plugin logicanalyzer by USB
- press reset and update simutaniously to boot into update mode
- update firmware by: sudo ./ols-loader -write -erase -p:/dev/ttyACM0 -wB:../FPGAROM/logic_sniffer_3.07-Demon-Core.bit
- next update the pic
- jumper PGC and PGD and reconnect usb to put the pic into update mode
- update firmware by:
- ols-fw-update -e -w -m flash -vid 0x04D8 -pid 0xFC90 -ix ../PIC_firmware/OLSv2.firmware.v3.0.hex
(in my case this ends with a segfault which is not an issue








The OpenBench Logic Sniffer is a $50 Open Source Logic Analyzer developed in collaboration between Gadget Factory (www.gadgetfactory.net) and Dangerous Prototypes (www.dangerousprototypes.com). 

Overview
--------
This git repository is a super project to bring together all of the Openbench Logic Sniffer projects into one place. It contains a master build script and all of the subprojects that comprise the software for the OLS.


Purchase
--------
[Gadget Factory](http://www.gadgetfactory.net/index.php?main_page=product_info&cPath=10&products_id=30)
[Seeed Studio](http://www.seeedstudio.com/depot/preorder-open-workbench-logic-sniffer-p-612.html?cPath=75)

Prerequisites
-------------
Before building ensure you have the following installed:
	* git, make, gcc-mingw, g++ (get these with cygwin for Windows)
	* perl
	* unzip, zip
	* ant (ant.apache.org)
	* maven

Build
-----
git clone git://github.com/GadgetFactory/OpenBench-Logic-Sniffer.git
cd build
ant update
ant build
ant run
ant dist

run 'ant help' to see options.
