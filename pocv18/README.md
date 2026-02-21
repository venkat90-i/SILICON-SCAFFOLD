# Silicon scaffold IDE (POC v18)

**Silicon scaffold IDE v18** (internally designated as the "Half-Stable Synthesis" build) marks the experimental beginning of true hardware synthesis integration. This release attempts to bridge the gap between RTL simulation and physical design mapping, though it comes with major instability.

---

##  CRITICAL KNOWN ISSUE: SDC,SYNTHESIS & GTKWAVE CRASHES.

**Be warned: The developer has explicitly marked this build as `!!!!CRASHES WITH SDC FILE ISSUES, LATEST HALF_STABLE!!!!`**. 
* The IDE now attempts to parse and integrate **.sdc (Synopsys Design Constraints)** files to pass timing constraints to the synthesis engine.
* There is a critical architectural bug in how these constraint files are being generated or read, causing the entire application to crash during the synthesis pipeline.
* **Do not use this version for production coding.**

---

##  What's New in POC v18 (Experimental Improvements)

Despite the crashes, this version lays the structural foundation for turning code into actual silicon:

### 1. Introduction of Logic Synthesis
* **Previous Constraint:** Up to v16, the IDE was strictly a simulation and schematic visualization tool. It could test if your code worked, but could not map it to physical hardware cells.
* **v18 Improvement:** This version officially initiates the **Synthesis Flow**. The backend is being wired to take your Verilog `.v` files and convert the behavioral logic into a structural gate-level netlist.

### 2. SDC (Timing Constraints) Scaffolding
* **Hardware Timing Requirements:** To synthesize hardware correctly, the compiler needs to know your target clock frequencies, input delays, and output loads.
* **v18 Improvement:** The IDE begins building the infrastructure to handle `.sdc` files. This allows the user to define these physical parameters. *(Note: This specific implementation is what is currently causing the IDE to crash).*

### 3. Retention of Core Stability
* While the new synthesis engine is highly unstable, the core text editor completely retains the robust `bridge_numpad` logic, deep regex syntax highlighting, and `autoseparators=True` undo/redo stack from the previous stable builds.

* ---
* ## 📥 Setup and Installation

### For Linux (Native) & WSL
Ensure you have the following packages installed based on your distribution.

```bash
sudo dnf update
# Install Python, UI, and Image components
sudo dnf install python3-tkinter python3-pillow-tk
# Install EDA Toolchain
sudo dnf install iverilog gtkwave yosys graphviz
