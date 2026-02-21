# Silicon scaffold IDE (POC v17)

**Silicon scaffold IDE v17** (internally designated as "The Librarian" build) represents a massive leap for the project, officially bridging the gap between RTL simulation and actual hardware realization. This version introduces a full, end-to-end Logic Synthesis flow with Process Design Kit (PDK) integration and a professional-grade workspace architecture.

---

##  What's New in POC v17 (Improvements)

This release elevates the IDE from a simple coding tool into a complete ASIC/FPGA frontend environment compared to v16:

### 1. Full Logic Synthesis Flow (F4)
* **PDK Integration:** The `⚙ Settings` menu now includes a selector for a **PDK Library (.lib)** file. This allows you to map your Verilog code to actual physical standard cells (like the Skywater 130nm or generic CMOS libraries).
* **The `F4` Engine:** Pressing `F4` (or clicking the new "Synth" button) triggers the `run_synthesis_flow` engine. It automatically runs a complex Yosys script (`synth`, `dfflibmap`, `abc` for tech mapping) to convert your behavioral RTL into a mapped structural gate-level netlist. 
* **Area Estimation:** After synthesis, the IDE automatically parses the Yosys output log to extract the estimated "Chip Area" and saves it as a dedicated report.

### 2. Interactive Constraint Wizard (SDC Generator)
* **GUI-Driven Constraints:** Before synthesis runs, a custom **Constraint Wizard** popup appears. You no longer need to write Synopsys Design Constraints (SDC) by hand.
* **Parameters:** You can easily input physical design targets like:
  * Clock Port Name & Frequency (MHz).
  * Input & Output Delays (ns).
  * Max Fanout & Load Capacitance (pF).
* The IDE automatically generates a perfectly formatted `.sdc` file and attaches it to your project for timing analysis.

### 3. Professional Workspace Architecture ("The Librarian")
* **Previous Constraint:** The Auto-Organizer in v16 simply dumped all files into a single `module_project/` folder.
* **v17 Improvement:** The `ensure_project_workspace` engine now enforces a strict, industry-standard VLSI directory structure. When you compile or synthesize, it creates:
  * `source/`: All your `.v` and testbench files are automatically isolated here.
  * `netlist/`: The generated gate-level Verilog (`_netlist.v`) and `.sdc` constraint files are saved here.
  * `reports/`: Synthesis logs (`synthesis.log`) and area reports (`area.rpt`) are neatly filed away here.

### 4. Smart Top-Module Detection
* **Mathematical Deduction:** To support synthesis, the IDE must know exactly which module is the "Top" design. Instead of guessing based on file names, v17 introduces the `find_top_module()` algorithm.
* **How it works:** It uses Regular Expressions to scan all Verilog files in your `source` directory. It creates a list of all *defined* modules and subtracts all *instantiated* modules. The remaining module that is defined but never instantiated anywhere else is mathematically guaranteed to be your Top Module, and the IDE automatically passes this to the Yosys synthesis engine.

* --
* ##  Setup and Installation

### For Linux (Native) & WSL
Ensure you have the following packages installed based on your distribution.

```bash
sudo dnf update
# Install Python, UI, and Image components
sudo dnf install python3-tkinter python3-pillow-tk
# Install EDA Toolchain
sudo dnf install iverilog gtkwave yosys graphviz
