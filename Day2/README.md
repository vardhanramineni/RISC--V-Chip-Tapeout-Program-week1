
# Day 2 -Timing libs,hierarchical vs flat synthesis and efficient flop coding styles
 

This session focuses on **understanding standard cells, .lib files, and synthesis flow using Yosys** with the **Sky130 PDK**.  

---

## Table of Contents  
- Standard Cells Overview  
- .lib File Introduction
- Hierarchical vs Flat Synthesis
- Various Flop Coding Styles and optimization 
- Outcome  

---

##  Standard Cells Overview  
- Basic building blocks used in ASIC design (e.g., INV, AND, OR, DFF).  
- Provided by the **Sky130 PDK** as a library.  
- Each cell has **function, area, delay, and power** characteristics.  

---

## .lib File Introduction  
- The `.lib` file describes standard cell characteristics:  
  - Timing arcs  
  - Power consumption  
  - Area  
  - Functionality  
- Used by **synthesis tools** (like Yosys) to map RTL → standard cells.  

---

## Hierarchical vs Flat Synthesis


### Hierarchical Synthesis 
- Each submodule is synthesized separately, then connected at the top.
- Easier debugging, reuse, and modularity.
```bash
$yosys
$read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
$read_verilog multiple_modules.v
$synth -top top_module
$abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
$write_verilog hierarchical_netlist.v
show
```
![Alt Text](Image/hier.png)
### Flat Synthesis 
- Flattens the design by removing module hierarchy.
- Synthesizes entire design as one large netlist.
```bash
$yosys
$read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
$read_verilog multiple_modules.v
$synth -top multiple_modules
$abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
$flatten
$show
```
![Alt Text](Image/flat.png)

##  Various Flop Coding Styles and optimization 

### Synchronous Reset (sync reset)

- Reset happens only on clock edge.
```bash
$iverilog dff_sync.v tb_dff_sync.v -o sync.out
$./a.out
$gtkwave tb_dff_sync.vcd
```

![Alt Text](Image/flat.png)

##  Outcome  

By the end of **Day 2**, we have:  
- Understood **standard cells** and **.lib files**.  
- Performed RTL → Gate-level synthesis using **Yosys**.  
- Generated netlist mapped to **Sky130 cells**.  

**Flow Recap:**  
**RTL → .lib → Yosys → Synthesized Netlist**

---
