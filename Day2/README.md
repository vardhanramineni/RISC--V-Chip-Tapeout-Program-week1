#!/bin/bash

# ==WEEK1 DAY2==  

This session focuses on **understanding standard cells, .lib files, and synthesis flow using Yosys** with the **Sky130 PDK**.  

---

## 📂 Table of Contents  
- Standard Cells Overview  
- .lib File Introduction  
- Lab Work with Yosys  
- Outcome  

---

## 🔹 Standard Cells Overview  
- Basic building blocks used in ASIC design (e.g., INV, AND, OR, DFF).  
- Provided by the **Sky130 PDK** as a library.  
- Each cell has **function, area, delay, and power** characteristics.  

---

## 🔹 .lib File Introduction  
- The `.lib` file describes standard cell characteristics:  
  - Timing arcs  
  - Power consumption  
  - Area  
  - Functionality  
- Used by **synthesis tools** (like Yosys) to map RTL → standard cells.  

---

## 🛠️ Lab Work with Yosys  

Start yosys:  
\`\`\`bash
$ yosys
\`\`\`

Read the **Sky130 library**:  
\`\`\`bash
yosys> read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
\`\`\`

Read RTL design:  
\`\`\`bash
yosys> read_verilog good_mux.v
\`\`\`

Run synthesis:  
\`\`\`bash
yosys> synth -top good_mux
\`\`\`

Map design to standard cells:  
\`\`\`bash
yosys> abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
\`\`\`

View schematic:  
\`\`\`bash
yosys> show
\`\`\`

Write synthesized netlist:  
\`\`\`bash
yosys> write_verilog good_mux_netlist.v
\`\`\`

Write simplified netlist:  
\`\`\`bash
yosys> write_verilog -noattr good_mux_netlist.v
\`\`\`

---

## ✅ Outcome  

By the end of **Day 2**, we have:  
- Understood **standard cells** and **.lib files**.  
- Performed RTL → Gate-level synthesis using **Yosys**.  
- Generated netlist mapped to **Sky130 cells**.  

**Flow Recap:**  
**RTL → .lib → Yosys → Synthesized Netlist**

---
EOF


# --- Git Setup ---
git init -q
git add .
git commit -m "Week1 Day2: Standard Cells, .lib, and Yosys synthesis flow" -q

echo "✅ Week1 Day2 repo created with README, Verilog files, and Git initialized."

