# Silicon scaffold IDE (POC v14)

**Silicon scaffold IDE v14** (internally designated as the "Auto-Organizer" build) introduces a radical change to file management. This version transforms the IDE from a simple file editor into a smart workspace manager that automatically structures your raw code into organized project folders.

---

##  What's New in POC v14 (Improvements)

This release focuses heavily on workspace cleanliness and project isolation compared to v13:

### 1. Workspace Auto-Organizer ("The Brain")
* **Previous Constraint:** If a user created multiple different modules (e.g., `alu.v`, `mux.v`, `cpu.v`) and their testbenches in the same folder, the directory would quickly become a chaotic mess of source files and generated build artifacts.
* **v14 Improvement:** The IDE now features an `ensure_project_folder` engine. When you click "Compile" or "Schematic", the IDE reads your file to determine the module name. It then automatically creates a dedicated subfolder (e.g., `alu_project/`) and physically moves your design file and its associated testbench into that new folder. 

### 2. Isolated Project Execution
* **Safe Compilations:** Because files are now automatically sorted into project folders, the IDE executes all backend tools (`iverilog`, `vvp`, `yosys`) strictly *inside* those specific subdirectories. 
* **Result:** Build artifacts like `.out`, `.vcd`, and `.png` files are generated cleanly inside their respective project folders, entirely preventing files from different modules from overwriting each other or cluttering the root directory.

### 3. Safe Root Maintenance Tool
* **Previous Constraint:** The old "Clean" button on the toolbar was a blunt instrument that wiped all generated files everywhere. With the new folder structure, this was deemed too risky.
* **v14 Improvement:** The "Clean" button has been completely removed from the top toolbar. It is replaced by a safe **"Clear Root Directory"** button located inside the `⚙ Settings` menu. 
* **Targeted Cleaning:** This new maintenance tool intelligently sweeps the root workspace for stray `.out`, `.vcd`, `.json`, `.log`, and `.history` files, but explicitly *protects* and ignores all contents inside your generated project folders.
* ---

* ##  Setup and Installation

### For Linux (Native) & WSL
Ensure you have the following packages installed based on your distribution.

```bash
sudo dnf update
# Install Python, UI, and Image components
sudo dnf install python3-tkinter python3-pillow-tk
# Install EDA Toolchain
sudo dnf install iverilog gtkwave yosys graphviz
