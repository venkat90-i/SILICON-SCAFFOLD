# silicon scaffold Workbench (POC v2)

**silicon scaffold  Workbench v2** is a multi-threaded Integrated Development Environment (IDE) designed for VLSI design and simulation. Whether running on a native **Linux** environment or within **Windows Subsystem for Linux (WSL)**, version 2 provides a responsive, graphical interface for professional EDA toolchains.

---

##  Key Advantages

* **Asynchronous Processing**: Background threading ensures the GUI remains responsive while simulations run.
* **Hardware Visualization**: Instantly render RTL code into gate-level schematics.
* **Unified Environment Support**: Compatible with Fedora, Ubuntu, and other Linux environments, as well as WSLg.
* **Real-Time Monitoring**: Streams live simulation logs directly to the integrated terminal.

---

##  Technical Specifications

| Component | Specification |
| :--- | :--- |
| **Language** | Python 3 with Tkinter GUI |
| **Display** | 1400x900 Optimized Workspace |
| **Threading** | Queue-based non-blocking execution |
| **Environments** | Linux (Ubuntu/Fedora/Debian) & WSL |
| **EDA Toolchain** | Icarus Verilog, GTKWave, Yosys, Graphviz |

---

##  Core Functionalities

### 1. Multi-Pane Integrated Layout
The workbench organizes your workflow into four primary sections:
* **File Explorer**: View and manage project `.v` files in your current directory.
* **Verilog Editor**: A dedicated space for writing and editing hardware descriptions.
* **Schematic Pane**: Renders visual diagrams of your logic gates using Yosys and Graphviz.
* **Terminal**: A bottom-docked, read/write console for system logs and interactive simulations.



### 2. Live Schematic Generation
Unlike standard text editors, Silis v2 can convert RTL code into a visual PNG schematic. This feature uses **Yosys** to synthesize the logic and **Graphviz** to create a searchable, visual diagram of the circuit architecture.

### 3. Threaded Simulation Engine
Simulation tasks are offloaded to background threads. This allows you to:
* Continue editing code while the simulation runs.
* See live output in the terminal as the `vvp` engine executes.
* Avoid the "Application Not Responding" errors common in single-threaded tools.

### 4. Smart Workspace Tools
* **Artifact Cleanup**: A dedicated  **Clean Artifacts** tool to wipe temporary build files (`.vcd`, `.out`, `.dot`, `.png`) with one click.
* **Automatic Wave Detection**: The tool automatically finds the latest `.vcd` file in your directory to open in GTKWave.

---

##  Setup and Installation

### For Linux (Native) & WSL
Ensure you have the following packages installed based on your distribution:

**Fedora / RHEL / CentOS:**
```bash
sudo dnf update
sudo dnf install python3-tkinter iverilog gtkwave yosys graphviz
