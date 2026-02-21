# Silicon scaffold Workbench (POC v3)

**Silicon scaffold Workbench v3** is an advanced, multi-threaded Integrated Development Environment (IDE) designed to streamline the VLSI design and simulation workflow within native **Linux** or **Windows Subsystem for Linux (WSL)**. Version 3.1 introduces true multi-file compilation, interactive terminal inputs, and a custom image rendering engine.

---

##  Improvements

* **True Multi-File Compilation**: Automatically detects and compiles all `.v` files in your project directory at once.
* **Interactive Terminal (STDIN)**: Send live input directly to running simulations (e.g., for user prompts or `$readmem`).
* **Advanced Hardware Visualization**: A custom-built rendering engine powered by Pillow (PIL) allows you to pan and seamlessly zoom into massive gate-level schematics.
* **X-Server Cursor Fix**: Forces standard cursor visibility to prevent the "invisible mouse" bug common in WSLg and X-Server environments.

---
##  CRITICAL KNOWN ISSUE: SCHEMATIC VIEWER IS BROKEN

**Be warned: The Schematic Viewer in v3.1 is currently unstable.** While the new zoom/pan GUI engine is fully implemented, the underlying generation pipeline from Yosys to Graphviz is failing. 
* You may experience errors where the `.dot` file is not generated or the `.png` conversion fails entirely. 
* Yosys may also fail to automatically resolve the top module using the `hierarchy -auto-top` command. 
* **Do not rely on the "Schematic (Yosys)" button in this build until a hotfix is deployed.**
---


## Technical Specifications

| Component | Specification |
| :--- | :--- |
| **Language** | Python 3 with Tkinter GUI and Pillow (PIL) |
| **Display** | 1400x900 Optimized Workspace |
| **Threading** | Subprocess Popen with separated stdin/stdout queues |
| **Compilation Scope** | Project-wide (`glob.glob("*.v")`) |
| **EDA Toolchain** | Icarus Verilog, GTKWave, Yosys, Graphviz |

---

##  Core Functionalities

### 1. Multi-Pane Integrated Layout
The workbench organizes your workflow into an expanded four-pane section:
* **File Explorer**: View and manage project `.v` files in your current directory.
* **Verilog Editor**: A dedicated space for writing and editing hardware descriptions.
* **Schematic Pane (Zoomable)**: A custom viewport that allows left-click dragging to pan and mouse-wheel scrolling to zoom in/out of logic diagrams.
* **Interactive Terminal**: A bottom-docked console split into a read-only output log and a dedicated `INPUT >` bar for two-way communication.

### 2. Project-Wide Compilation
Unlike previous versions that only compiled the currently active tab, Silis v3.1 automatically targets all Verilog files in your working directory. Clicking "Run (Iverilog)" links all modules and testbenches together seamlessly before executing the `vvp` engine.

### 3. Threaded Interactive Simulation
Simulation tasks are offloaded to background threads with open standard input pipes. This allows you to:
* Type values into the `INPUT >` bar and hit Enter to feed data live to your Verilog testbench.
* See live standard output and standard error stream into the terminal log.
* Continue editing code without the application freezing.

### 4. Smart Workspace Tools
* **Artifact Cleanup**: A dedicated  **Clean** tool to wipe temporary build files (`.vcd`, `.out`, `.dot`, `.png`, `.history`) with one click.
* **Automatic Wave Detection**: The tool automatically finds the latest generated `.vcd` file in your directory to launch in GTKWave.

---

## Setup and Installation

### For Linux (Native) & WSL
Ensure you have the following packages installed based on your distribution. **Note: v3.1 requires new Pillow (PIL) dependencies for the zoomable schematic viewer.**


```bash
sudo dnf update
# Install Python, UI, and Image components
sudo dnf install python3-tkinter python3-pillow-tk
# Install EDA Toolchain
sudo dnf install iverilog gtkwave yosys graphviz
