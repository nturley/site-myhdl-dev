---
title:  Initial values support
author: Christopher Felton
layout: wide_article
---

This page was created to keep track of the status of the initial value support.  
The original open task description is available [here][/tasks/initial-values-support].

Below is a summary from the mailing-list.

Enabling Initial Value Support
------------------------------

Initial value support can be re-enabled.  The Verilog
upport of initial values was verified with the latest
version of Quartus.

Need to test with (list syn and sim tools)?

* [x] Quartus latest
* [ ] ISE (xst) latest
* [ ] cver
* [ ] icarus

See below for some preliminary results.

Function Attributes to Disable Initial Values
---------------------------------------------

None will *not* be added to intbv.  An argument will
be added to the toVerilog and toVHDL to disable
"plain" Signal init and "memory" (array) init.
Something like the following.

    toVerilog(... disable_init=False, disable_mem_init=False)
    toVHDL( "" "" )

Arguments can always be used as ports, so configuration
should go elsewhere. Currently function attributes are for
such purposes:

    toVerilog.disable_init = False


toVerilog Initial Values
------------------------

toVerilog will only create initial values for Signals converted to register
types.


Initial Values for Memories
---------------------------

Initial values for memories (list of signals) will be
generated.  If feasible the synthesizable versions 
of the memory init values will be generated [1].

Some Results
------------

### Altera Quartus (11.1sp2) Verilog

  1. Initial values.  The reg initial values don't
     error during synthesis (added these manually).

  2. The initial block for RAM init values didn't
     error during synthesis and generated initial
     values for the RAM (generated a .mif file with
     the correct init values).

  3. ROM *no* BRAM used for ROM tested at size
     8x2048?

### Altera Quartus (11.1sp2) VHDL

  TBC

### Xilinx ISE (13.4) Verilog

  1. Initial values.  The reg initial values don't
     error during synthesis (added these manually).

  2. The initial block for RAM init values didn't
     error during synthesis.  Not clear if the 
     initial values would be loaded (file generated)

  3. TBD

### Xilinx ISE (13.4) VHDL
  TBC 

  
@todo : create a table for the above information.

Some test code here: <https://bitbucket.org/cfelton/examples/src/tip/ramrom>

[1]: http://www.altera.com/literature/hb/qts/qts_qii51007.pdf
