sigmet_raw
==========

INTRODUCTION
    The sigmet_raw program accesses Sigmet data, specifically radar data from raw product
    files produced by Sigmet RVP signal processors. See:
    https://www.vaisala.com/en/products/instruments-sensors-and-other-measurement-devices/weather-radar-products/rvp900
    The Sigmet raw product file format is documented at:
    ftp://ftp.sigmet.com//outgoing/manuals/IRIS-Programming-Guide-M211318EN.pdf
    (Fetch with a ftp client like ftp or curl, not with a web browser.)

PROGRAM:
    sigmet_raw runs as a command line utility. A call usually reads a Sigmet raw product
    file and prints headers and data to standard output as specified in command line
    arguments. For more information, install the program and run:
	sigmet_raw
	    Without arguments, prints release information and pointers to more information.
	sigmet_raw man sigmet_raw
	sigmet_raw help # (same as "sigmet_raw man sigmet_raw")
	    Prints the sigmet_raw man page.
	sigmet_raw subcommands
	    Lists the subcommands with brief descriptions and pointers to more documentation.
	    A subcommand is the first word on the command line after "sigmet_raw".
	sigmet_raw man subcommand
	    Displays a man page for subcommand, if available. Some subcommands are shell
	    scripts with documentation in the script.
    Typical usage looks like:
	sigmet_raw sweep_headers raw_product_file
	sigmet_raw data DB_DBZ 2 raw_product_file
    The above calls read raw_product_file and print sweep headers and reflectivity data
    to standard output. Note that the above sequence reads the raw_product_file twice,
    which can be slow. For faster interaction, run:
	sigmet_raw vol_dmn socket_path raw_product_file
    This starts a daemon process that reads raw_product_file and then listens to
    socket_path for subcommands. Then go:
	sigmet_raw sweep_headers socket_path
	sigmet_raw data DB_DBZ 2 socket_path
    This produces the same output without reading raw_product_file twice. When done,
    terminate the daemon with:
	sigmet_raw exit socket_path
    or delete the socket. Daemon usage is faster. On the downside, daemons run forever. To
    keep immortal orphan daemons from taking over the system, put the commands into a
    shell script that looks like:
	#!/bin/sh
	sigmet_raw sweep_headers $SIGMET_RAW_SKT
	sigmet_raw data DB_DBZ 2 $SIGMET_RAW_SKT
    Then run:
	sigmet_raw shell raw_product_file script [args ...]
    This will start a daemon, run script with the socket path automatically placed in
    the SIGMET_RAW_SKT environment variable, and then terminate the daemon on exit.

SYSTEM REQUIREMENTS:
    Standard Unix system, as described in:
	http://pubs.opengroup.org/onlinepubs/9699919799/toc.htm
    This is the Single Unix Specification, also known as:
	POSIX.1-2008
	IEEE Std 1003.1-2008
	The Open Group Technical Standard Base Specifications, Issue 7, 2018 edition.
    Standard C compiler, as described in:
	ISO/IEC 9899:2018(E)
    The software should build and run on any GNU/Linux, BSD, or MacOS X system.

TO BUILD AND INSTALL:
    Set current working directory to the directory that contains this README.
    Run one of these:
	./configure
	./configure --prefix=DIR
    The first call arranges to install the software libraries, and documentation in
    /usr/local. The second call arranges to put everything into DIR (e.g. $HOME/local),
    with the sigmet raw executable will ending up in DIR/bin.
    After running configure, build the software with:
	make
    If all goes well, install everything with:
	make install
    For customizations run configure and edit Makefile and src/Makefile.

LICENSE:
    The software is distributed under the terms of the Academic Free License,
    in AFL-3.0. Please email feedback to Gordon Carrie dev1960@polarismail.net.

MANIFEST:
    ".configure --prefix=${PREFIX};make install" installs the below listed files.
    YYYYMMDDHHMMSS identifies this release. It is the suffix of this directory.
	${PREFIX}/bin/sigmet_raw
	${PREFIX}/lib/sigmet_raw/YYYYMMDDHHMMSS/AFL-3.0
	${PREFIX}/lib/sigmet_raw/YYYYMMDDHHMMSS/RELEASE_NOTES
	${PREFIX}/lib/sigmet_raw/YYYYMMDDHHMMSS/RELEASE_TIMESTAMP
	${PREFIX}/lib/sigmet_raw/YYYYMMDDHHMMSS/bin/bdata
	${PREFIX}/lib/sigmet_raw/YYYYMMDDHHMMSS/bin/data
	${PREFIX}/lib/sigmet_raw/YYYYMMDDHHMMSS/bin/data_types
	${PREFIX}/lib/sigmet_raw/YYYYMMDDHHMMSS/bin/difftime
	${PREFIX}/lib/sigmet_raw/YYYYMMDDHHMMSS/bin/env
	${PREFIX}/lib/sigmet_raw/YYYYMMDDHHMMSS/bin/exit
	${PREFIX}/lib/sigmet_raw/YYYYMMDDHHMMSS/bin/good
	${PREFIX}/lib/sigmet_raw/YYYYMMDDHHMMSS/bin/help
	${PREFIX}/lib/sigmet_raw/YYYYMMDDHHMMSS/bin/man
	${PREFIX}/lib/sigmet_raw/YYYYMMDDHHMMSS/bin/mk_case
	${PREFIX}/lib/sigmet_raw/YYYYMMDDHHMMSS/bin/near_sweep
	${PREFIX}/lib/sigmet_raw/YYYYMMDDHHMMSS/bin/normaltm
	${PREFIX}/lib/sigmet_raw/YYYYMMDDHHMMSS/bin/prf
	${PREFIX}/lib/sigmet_raw/YYYYMMDDHHMMSS/bin/ray_headers
	${PREFIX}/lib/sigmet_raw/YYYYMMDDHHMMSS/bin/release
	${PREFIX}/lib/sigmet_raw/YYYYMMDDHHMMSS/bin/shell
	${PREFIX}/lib/sigmet_raw/YYYYMMDDHHMMSS/bin/sigmet_raw
	${PREFIX}/lib/sigmet_raw/YYYYMMDDHHMMSS/bin/sizex
	${PREFIX}/lib/sigmet_raw/YYYYMMDDHHMMSS/bin/subcommands
	${PREFIX}/lib/sigmet_raw/YYYYMMDDHHMMSS/bin/sweep_headers
	${PREFIX}/lib/sigmet_raw/YYYYMMDDHHMMSS/bin/uniq
	${PREFIX}/lib/sigmet_raw/YYYYMMDDHHMMSS/bin/uniq.awk
	${PREFIX}/lib/sigmet_raw/YYYYMMDDHHMMSS/bin/vel_ua
	${PREFIX}/lib/sigmet_raw/YYYYMMDDHHMMSS/bin/vol_dmn
	${PREFIX}/lib/sigmet_raw/YYYYMMDDHHMMSS/bin/vol_hdr
	${PREFIX}/lib/sigmet_raw/YYYYMMDDHHMMSS/bin/vol_hdrs
	${PREFIX}/lib/sigmet_raw/YYYYMMDDHHMMSS/bin/vol_id
	${PREFIX}/lib/sigmet_raw/YYYYMMDDHHMMSS/bin/vol_in_dt
	${PREFIX}/lib/sigmet_raw/YYYYMMDDHHMMSS/bin/vol_tm
	${PREFIX}/lib/sigmet_raw/YYYYMMDDHHMMSS/bin/vol_tm.awk
	${PREFIX}/lib/sigmet_raw/YYYYMMDDHHMMSS/bin/volume_headers
	${PREFIX}/lib/sigmet_raw/YYYYMMDDHHMMSS/bin/volume_headers_desc
	${PREFIX}/lib/sigmet_raw/YYYYMMDDHHMMSS/bin/ymds_time
	${PREFIX}/lib/sigmet_raw/YYYYMMDDHHMMSS/libexec/vol_hdrs.awk
	${PREFIX}/lib/sigmet_raw/YYYYMMDDHHMMSS/libexec/vol_in_dt
	${PREFIX}/lib/sigmet_raw/YYYYMMDDHHMMSS/share/doc/README
	${PREFIX}/lib/sigmet_raw/YYYYMMDDHHMMSS/share/doc/volume_headers
	${PREFIX}/lib/sigmet_raw/YYYYMMDDHHMMSS/share/man/man1/bdata.1
	${PREFIX}/lib/sigmet_raw/YYYYMMDDHHMMSS/share/man/man1/data.1
	${PREFIX}/lib/sigmet_raw/YYYYMMDDHHMMSS/share/man/man1/data_types.1
	${PREFIX}/lib/sigmet_raw/YYYYMMDDHHMMSS/share/man/man1/difftime.1
	${PREFIX}/lib/sigmet_raw/YYYYMMDDHHMMSS/share/man/man1/exit.1
	${PREFIX}/lib/sigmet_raw/YYYYMMDDHHMMSS/share/man/man1/good.1
	${PREFIX}/lib/sigmet_raw/YYYYMMDDHHMMSS/share/man/man1/normaltm.1
	${PREFIX}/lib/sigmet_raw/YYYYMMDDHHMMSS/share/man/man1/ray_headers.1
	${PREFIX}/lib/sigmet_raw/YYYYMMDDHHMMSS/share/man/man1/sigmet_raw.1
	${PREFIX}/lib/sigmet_raw/YYYYMMDDHHMMSS/share/man/man1/sweep_headers.1
	${PREFIX}/lib/sigmet_raw/YYYYMMDDHHMMSS/share/man/man1/vel_ua.1
	${PREFIX}/lib/sigmet_raw/YYYYMMDDHHMMSS/share/man/man1/vol_dmn.1
	${PREFIX}/lib/sigmet_raw/YYYYMMDDHHMMSS/share/man/man1/vol_in_dt.1
	${PREFIX}/lib/sigmet_raw/YYYYMMDDHHMMSS/share/man/man1/volume_headers.1
	${PREFIX}/lib/sigmet_raw/YYYYMMDDHHMMSS/share/man/man3/sigmet_data.3
	${PREFIX}/lib/sigmet_raw/YYYYMMDDHHMMSS/share/man/man3/sigmet_raw.3
	${PREFIX}/lib/sigmet_raw/YYYYMMDDHHMMSS/share/man/man3/sigmet_vol.3

