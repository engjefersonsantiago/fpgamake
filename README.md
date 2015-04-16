fpgamake
========

    usage: fpgamake [-h] [-o OUTPUT] [-s SYNTH] [--xci XCI] [--xdc XDC]
		    [--floorplan FLOORPLAN] [-t TOP] [-b BITFILE] [-v VERBOSE]
		    vpath [vpath ...]

    Generates Makefiles to synthesize, place, and route verilog. Each module
    specified will be synthesized into a separate design checkpoint. If a
    floorplan is provided, each instance of the synthesized modules will be
    separately placed and routed and then combined into the top level design.

    positional arguments:
	vpath                 Verilog path

    optional arguments:
	-h, --help            show this help message and exit
	-o OUTPUT, --output OUTPUT
			      Output make file
	-s SYNTH, --synth SYNTH
			      Module to synthesize separately
	--xci XCI             XCI file to use
	--xdc XDC             XDC file to use
	--floorplan FLOORPLAN
			      Floorplan XDC.
	-t TOP, --top TOP     Top verilog file
	-b BITFILE, --bitfile BITFILE
			      Bit file to generate
	-v VERBOSE, --verbose VERBOSE
			      Verbose operation

Installation
------------

From Ubuntu packages:

    sudo apt-add-repository -y ppa:jamey-hicks/connectal
    sudo apt-get update
    sudo apt-get -y install fpgamake

From RPM packages, install the appropriate repo file:

* http://download.opensuse.org/repositories/home:/jameyhicks:/connectal/CentOS_7/home:jameyhicks:connectal.repo
* http://download.opensuse.org/repositories/home:/jameyhicks:/connectal/RHEL_7/home:jameyhicks:connectal.repo
* http://download.opensuse.org/repositories/home:/jameyhicks:/connectal/Fedora_20/home:jameyhicks:connectal.repo
    
    yum install fpgamake

From Github:

    git clone https://github.com/cambridgehackers/fpgamake
    git clone https://github.com/cambridgehackers/buildcache

Xilinx KC705 Example
--------------------

Check out or download the fpgamake sources, as above.

    cd examples/uart_kc705; make all

This example requires the BSV compiler.

Altera Terasic DE5 Example
--------------------------

Check out or download the fpgamake sources, as above.

    cd examples/uart_de5; make all

This example requires the BSV compiler.

Vivado Tutorial TD
------------------

To build the Vivado Tutorial TD with fpgamake. Download and unpack the tutorial, and the run the following command:

    SOURCEDIR=/path/to/Vivado_Tutorial_TD/Sources
    XDCDIR=$SOURCEDIR/Sources/xdc
    ./fpgamake --board='noboard' --part='xc7k70tfbg676-2' -b top.bit -o fpgamake.mk -t top -s usbf_top -s or1200_top --floorplan=$XDCDIR/top_flpn.xdc --xdc=$XDCDIR/top.xdc --header=or1200_defines.v --header=usbf_defines.v $SOURCEDIR/hdl
    make -f fpgamake.mk
