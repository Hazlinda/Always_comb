# Always_comb
In an always block which is used to model combinational logic, forgetting an else leads to an unintended latch. To avoid this mistake, SystemVerilog adds specialized always_comb and always_latch blocks, which indicate design intent to simulation, synthesis and formal verification tools. SystemVerilog also adds an always_ff block to indicate sequential logic.

SystemVerilog provides a special always_comb procedure for modeling combinational logic behavior. For example:
    
    always_comb
    a = b & c;

    always_comb
    d <= #1ns b & c;
    
The always_comb procedure provides functionality that is different than a normal always procedure:
  — There is an inferred sensitivity list..
  — The variables written on the left-hand side of assignments shall not be written to by any other process.
  — The procedure is automatically triggered once at time zero, after all initial and always blocks have been started, so that the outputs     of the procedure are consistent with the inputs.

The SystemVerilog always_comb procedure differs from the Verilog-2001 always @* in the following ways:
  — always_comb automatically executes once at time zero, whereas always @* waits until a change occurs
    on a signal in the inferred sensitivity list.
  — always_comb is sensitive to changes within the contents of a function, whereas always @* is only sensitive
    to changes to the arguments of a function.
  — Variables on the left-hand side of assignments within an always_comb procedure, including variables
    from the contents of a called function, shall not be written to by any other processes, whereas always @* permits multiple processes     to write to the same variable.
  — Statements in an always_comb shall not include those that block, have blocking timing or event controls, or fork...join statements.

Software tools can perform additional checks to warn if the behavior within an always_comb procedure does
not represent combinational logic, such as if latched behavior can be inferred.

# Implicit always_comb sensitivities

The expansion of longest static prefix “P” is defined to be:
  a) P itself if the P is not a memory or indexing select or if P is a legal word or bit select.
  b) if P is a memory or indexing select, the expansion is every possible legal memory word select with a static prefix that matches P.

The implicit sensitivity list of an always_comb includes the expansions of the longest static prefix of each variable or select expression that is read within the block or within any function called within the block with the following exceptions:
  1) any expansion of a variable declared within the block or within any function called within the block.
  2) any expression that is also written within the block or within any function called within the block.
