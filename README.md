cIntelHex - A C library for parsing Intel HEX files
===================================================

Authors
-------

Martin Helmich <martin.helmich@hs-osnabrueck.de>  
Oliver Erxleben <oliver.erxleben@hs-osnabrueck.de>

University of Applied Sciences Osnabrück

License
-------

This program is free software: you can redistribute it and/or modify
it under the terms of the GNU Lesser General Public License as published by
the Free Software Foundation, either version 3 of the License, or
(at your option) any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU Lesser General Public License for more details.

You should have received a copy of the GNU Lesser General Public License
along with this program.  If not, see <http://www.gnu.org/licenses/>.

Synopsis
--------

libcintelhex is a C library for parsing Intel HEX files and mapping their
binary contents into application or device memory.

Installation
------------

### Requirements

libcintelhex has no requirements besides a halfway recent GCC and a C standard
library.

When cloning from Git, you will also need autoconf to generate the configure script.

### Compilation

Installation as usual:

	./configure
	make
	make install

Usage
-----

After installation, include `cintelhex.h` and add `-lcintelhex` to your linker flags.

### Reading Intel HEX data

This library can parse Intel HEX data either from an input file or directly
from a given string:

    ihex_records_t* r1 = ihex_from_file("my_filename");
    
    char* input = ":1a01000021A4B2Fe...";
    ihex_records_t* r2 = ihex_from_string(input);

### Applying Intel HEX data

Intel HEX data can be copied to any region in memory (either somewhere in RAM,
but also to mapped memory regions of hardware devices):

    void* dst = malloc(8192); // Allocate target region.
    int   r   = ihex_mem_copy(rs, dst, 8192,
        IHEX_WIDTH_32BIT, IHEX_ORDER_BIGENDIAN); // Copy data to target region.

    if (r == 0) printf("All is well.\n");
    else return r;
