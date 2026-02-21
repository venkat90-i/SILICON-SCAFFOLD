# Silicon scaffold Workbench (POC v4)

**Silicon scaffold Workbench v4** is a significant update to the Python-based IDE designed for VLSI engineering and RTL development. This release transforms the tool from a static single-directory script into a dynamic, multi-project IDE with a fully functional hardware visualizer and a dual-mode interactive terminal.

---

##  What's New in POC v4 (Improvements)

This version addresses critical bugs from v3.1 and introduces major quality-of-life upgrades for managing complex silicon design projects:

### 1. Dynamic Project Explorer & Directory Sync
* **Interactive File Tree:** The static file list has been replaced with a full-fledged directory explorer. You can now expand and collapse folders directly within the UI.
* **Auto-Sync CWD:** Double-clicking a folder or file automatically updates the IDE's Current Working Directory (CWD). This allows you to seamlessly switch between different design projects without restarting the application.

### 2. Dual-Mode Interactive Terminal
The bottom console is now a highly versatile, context-aware terminal featuring two distinct modes:
* **SHELL Mode:** Acts as a standard Linux Bash prompt. You can execute system commands (like `ls`, `mkdir`), manually compile files, and use standard **Tab Auto-Completion** for file and folder paths.
* **SIMULATION Mode:** Automatically engages when running a Verilog simulation. It explicitly routes your text inputs (`stdin`) to the active `vvp` process, allowing you to interact with `$readmem` or user prompts in real-time.

### 3. Smart Schematic Viewer (Bug Fixed)
* **Functional Rendering:** The critical image rendering bug from previous versions has been fixed. The schematic pipeline successfully uses Pillow (PIL) to scale, pan, and zoom the generated logic diagrams on the canvas.
* **Smart Synthesis Filtering:** The IDE now intelligently filters out testbench files (files starting with `tb_` or `test_`) before sending the design to Yosys. This prevents the synthesis engine from crashing on non-synthesizable Verilog constructs.

### 4. Robust Absolute Path Handling
* The underlying architecture has been rewritten to abandon relative paths. All file operations and backend tools (`iverilog`, `gtkwave`, `yosys`) now explicitly execute within the active `cwd`. This eliminates crashes caused by background directory navigation.

---

##  Technical Specifications

| Component | Specification |
| :--- | :--- |
| **Language** | Python 3 with Tkinter GUI & Pillow (PIL) |
| **File Management** | Native `os` and `glob` dynamic pathing |
| **Terminal Modes** | Subprocess `shell=True` (Bash) / Stdin Pipe (Sim) |
| **Synthesis Tool** | Yosys with smart `tb_` filtering |
| **EDA Toolchain** | Icarus Verilog, GTKWave, Yosys, Graphviz |

---

##  Core Functionalities

* **Project-Wide Compilation**: Clicking "Compile & Run" automatically links and compiles all `.v` files in your current working directory.
* **Live Hardware Visualization**: Generate gate-level schematic PNGs instantly with pan/zoom mouse controls.
* **Smart Artifact Cleanup**: The  **Clean** button sweeps the current directory of temporary build files (`.vcd`, `.out`, `.dot`, `.png`).
* **Threaded Execution**: Simulations run asynchronously in the background so the IDE never freezes.

---

##  Setup and Installation

### For Linux (Native) & WSL
Ensure you have the following packages installed based on your distribution. 


```bash
sudo dnf update
# Install Python, UI, and Image components
sudo dnf install python3-tkinter python3-pillow-tk
# Install EDA Toolchain
sudo dnf install iverilog gtkwave yosys graphviz
