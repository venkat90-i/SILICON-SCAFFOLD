# Silicon scaffold IDE (POC v25)

**Silicon scaffold IDE v25** (internally designated as the "Hierarchy Safe" build) tackles the final frontiers of hardware visualization and language support. This release ensures that massive, multi-module designs are rendered efficiently without crashing the IDE, and it officially introduces support for SystemVerilog.

---

##  What's New in POC v25 (Improvements)

This release implements intelligent safeguards for large-scale ASIC designs and expands the compiler's language capabilities compared to v24:

### 1. SystemVerilog (`.sv`) Integration
* **Previous Constraint:** The IDE only scanned for and compiled standard Verilog-2001 (`.v`) files.
* **v25 Improvement:** The compiler pipeline has been heavily upgraded to natively support SystemVerilog. 
* **Dual-Language Pipeline:** When you hit Compile or Synthesize, the IDE searches for both `.v` and `.sv` files. It automatically passes the `-g2012` flag to `iverilog` to enable SystemVerilog simulation, and it uses the `read_verilog -sv` command to ensure Yosys accurately synthesizes the advanced SV constructs.

### 2. "Hierarchy Safe" Schematic Generation
* **Previous Constraint:** Earlier versions used the generic Yosys `opt` command before generating schematics. For complex designs (like a CPU with ALUs and Registers), `opt` aggressively flattened the entire design into a giant, unreadable web of basic AND/OR gates.
* **v25 Improvement:** The IDE now implements a custom `HIER_CMD` (`hierarchy -check -top {base}; proc; opt_clean`). By explicitly using `opt_clean` instead of `opt`, Yosys removes unused wires but strictly preserves your module boundaries. Your schematic will now cleanly show "ALU" or "Register File" as distinct black-boxes instead of flattening them into gate-level spaghetti.

### 3. The "Big File Guard" (OOM Crash Prevention)
* **Previous Constraint:** Even with vector SVGs, attempting to render a multi-megabyte processor schematic would lock up the Qt rendering thread and crash the IDE.
* **v25 Improvement:** A strict `BIG FILE GUARD` has been added to the `SilisSchematic` viewer. Before loading the image into the canvas, it checks the file size. If the SVG exceeds 5.0 MB, it aborts the Qt rendering process. Instead, it safely prints a red warning on the canvas: *"Schematic Too Large... Open with Browser/KLayout"*, ensuring your workspace remains perfectly responsive.

### 4. Advanced Node.js Memory Limits & Fallbacks
* **Backend Stability:** `netlistsvg` runs on Node.js, which famously crashes on large JSON files due to V8 JavaScript memory limits.
* **v25 Improvement:** The IDE now explicitly injects `NODE_OPTIONS="--max-old-space-size=4096"` into the environment before triggering the schematic engine, allowing Node to use 4GB of RAM to process massive netlists.
* **Graceful Degradation:** A 15-second `timeout=15` has been added to the vector engine. If `netlistsvg` chokes or times out, the IDE catches the exception and gracefully falls back to the industrial `Graphviz` engine so you still get a visual output.
