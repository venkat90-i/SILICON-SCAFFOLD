# Silicon scaffold IDE (POC v13)

**Silicon scaffold IDE v13** (internally designated as the "Surgical VCD" build) introduces a highly intelligent, context-aware backend. This version fundamentally changes how the IDE interacts with your code, reading and understanding your Verilog modules to automate the most tedious parts of testing and visualization.

---

##  What's New in POC v13 (Improvements)

This release moves away from "generic project compilation" into "smart module targeting," vastly improving the simulation workflow compared to v12:

### 1. Context-Aware Module Parsing
* **Smart Detection:** The IDE now features a `get_context_target` engine. As soon as you hit "Compile" or "Schematic", the IDE parses the active editor window using Regular Expressions (`module\s+(\w+)`) to automatically figure out the exact name of the Design Under Test (DUT) or Testbench you are working on.
* **Automatic Linking:** If you are editing a design file (e.g., `alu.v`), the IDE automatically searches your project directory for its associated testbench (e.g., `tb_alu.v` or `alu_tb.v`) and links them for you.

### 2. "Surgical VCD" Auto-Injection (Massive Workflow Upgrade)
* **Previous Constraint:** In all previous versions, if a user forgot to manually write `$dumpfile("waves.vcd"); $dumpvars(0);` inside their testbench's `initial` block, the IDE would fail to generate waveforms, forcing the user to edit their code and recompile.
* **v13 Improvement:** The IDE now handles this for you. If it detects that your testbench is missing the dump commands, it creates a hidden, temporary testbench (`._temp_tb.v`). It uses a surgical Regex pattern to find your `initial begin` block and injects the waveform generation commands instantly in the background before compiling. 
* **Result:** You get GTKWave results every single time, perfectly automated.

### 3. Targeted Artifact Naming
* **Previous Constraint:** Schematics were always saved as `schematic.png` and simulations as `design.out`, meaning old files were constantly overwritten.
* **v13 Improvement:** Outputs are now strictly named after the detected module. If you synthesize an ALU, Yosys is instructed to use `hierarchy -check -top alu` and saves the file as `alu.png`. The simulation output is saved as `alu.vcd`. This allows you to keep multiple different schematics and waveforms in the same folder without conflicts.

### 4. Visual Toolbar Beacon (SK Indicator)
* **Visual Upgrade:** The Superkey (SK) indicator has been upgraded again to be much more obvious. When you press the leader key (`` ` ``), the entire top toolbar instantly flashes bright CYAN (`#00FFFF`), serving as an unmissable visual beacon that the IDE is awaiting your shortcut key. It cleanly resets to standard gray once the shortcut completes or times out.

* ---
* ##  Setup and Installation

### For Linux (Native) & WSL
Ensure you have the following packages installed based on your distribution

```bash
sudo dnf update
# Install Python, UI, and Image components
sudo dnf install python3-tkinter python3-pillow-tk
# Install EDA Toolchain
sudo dnf install iverilog gtkwave yosys graphviz
