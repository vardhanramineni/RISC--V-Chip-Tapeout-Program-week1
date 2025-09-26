#!/bin/bash
# ===============================
# Day 3 - Combinational & Sequential Optimizations
# ===============================

# Clean workspace
rm -f a.out *.vcd *.dot *.svg *.json *.out *_netlist.v

echo "=================================="
echo "THEORY: Combinational Optimizations"
echo "- Simplify Boolean equations"
echo "- Remove redundant gates"
echo "- Constant propagation"
echo "=================================="

echo "THEORY: Sequential Optimizations"
echo "- Remove unused flip-flops"
echo "- Optimize unused outputs"
echo "- Merge equivalent registers"
echo "=================================="

# ===============================
# Introduction to Optimizations (D3SK1 L1-L3)
# ===============================
yosys <<EOT
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog opt_intro.v
synth -top opt_intro
opt
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
write_verilog opt_intro_netlist.v
show
EOT

# ===============================
# Lab06 - Combinational Logic Optimisations (D3SK2 L1-L2)
# ===============================
yosys <<EOT
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog comb_opt.v
synth -top comb_opt
opt_clean
opt_reduce
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
write_verilog comb_opt_netlist.v
show
EOT

# ===============================
# Lab07 - Sequential Logic Optimisations (D3SK3 L1-L3)
# ===============================
yosys <<EOT
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog seq_opt.v
synth -top seq_opt
opt_clean
opt_muxtree
opt_share
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
write_verilog seq_opt_netlist.v
show
EOT

# ===============================
# Sequential Optimisation: Unused Outputs (D3SK4 L1-L2)
# ===============================
yosys <<EOT
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog seq_unused.v
synth -top seq_unused
opt_clean -purge
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
write_verilog seq_unused_netlist.v
show
EOT

echo "Day 3 flow completed: Combinational & Sequential Optimizations done."
