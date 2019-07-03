# Always_comb
In an always block which is used to model combinational logic, forgetting an else leads to an unintended latch. To avoid this mistake, SystemVerilog adds specialized always_comb and always_latch blocks, which indicate design intent to simulation, synthesis and formal verification tools. SystemVerilog also adds an always_ff block to indicate sequential logic.
