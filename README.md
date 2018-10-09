# altera-linux-pcie-driver
A linux PCIe driver for Altera

https://fpgawiki.intel.com/wiki/index.php?title=Linux_PCIe_driver&oldid=10208


Altera OpenCL PCI Express Driver for Linux
------------------------------------------

This directory contains full source code for the Altera OpenCL 
PCIE Express Driver for Linux [1][2].  

The driver achieves approximately 1410 MB/sec on gen2 x 4 PCIe 
core with SG DMA on Stratix IV GX FPGA (71% efficiency).


LIMITATIONS
-----------
Currently support a single board with a single FPGA on it. Only one single-
threaded user process should be accessing the driver at a time.

DMA controller supports operations on 32-byte aligned data (both source and
destination must be aligned). Furthermore, the size of the data must also
be 32-byte aligned. If any of these alignments are not met, very slow non-
DMA transfer will be used.


PREREQUISITES
-------------
- GCC version in /usr/bin (the same version of gcc that was used to compile
  the kernel).

- Kernel include files, or the complete source. The make script
  (make_all.sh) assumes that the source is installed in 
  /usr/src/kernels/<version>.


COMPIILE and INSTALL
--------------------

To compile the driver, run as regular user:
  sh make_all.sh


To load the compiled driver:
  sudo sh ./aclpci_load
(The driver must be loaded to run host programs AND to reprogram 
the device).

  
To quickly test if the driver and the board work
  ./user
(You should see "Done testing!" line at the end).


To unload the driver:
  sudo sh ./aclpci_unload


TESTING
-------
The driver was developed and tested on CentOS 5.6, 64-bit with 
2.6.18-238.el5 kernel compiled for x86_64 architecture.

Also tested on CentOS 6.2, 64-bit with 2.6.32-220.el6.x86_64 kernel.


FEEDBACK
--------
Issues, comments, enhancements? Contect Dmitry Denisenko at ddenisen@altera.com.


[1] Altera, Quartus, and Stratix are tradermarks of Altera Corporation.
[2] OpenCL and the OpenCL logo are trademarks of Apple Inc.
