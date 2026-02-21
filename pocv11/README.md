# Silicon scaffold IDE (POC v11)

**Silicon scaffold IDE v11** (internally designated as the "Silicon Scaffold" build) marks the official transition from a "Workbench" proof-of-concept into the fully branded **Silis IDE**. This milestone release completely overhauls the hardware visualization engine, introducing professional-grade IEEE schematic rendering and customizable visual themes.

---

##  What's New in POC v11 (Improvements)

This version focuses on vastly improving how you view and analyze your synthesized RTL designs compared to v10:

### 1. Dual-Engine Schematic Visualizer (NetlistSVG)
* **Previous Constraint:** In all previous versions, the IDE relied entirely on `Graphviz` to draw schematics. While functional, Graphviz only draws generic boxes and bubbles, making it difficult to read complex logic circuits.
* **v11 Improvement:** Silis now integrates a highly advanced **NetlistSVG** engine. 
* **How it works:** Instead of outputting a generic `.dot` file, Yosys is now instructed to generate a structured JSON netlist (`write_json`). The IDE passes this to `netlistsvg`, which renders the circuit using **true IEEE-standard logic gate shapes** (e.g., proper D-shaped AND gates, curved OR gates, distinct D-Flip-Flop blocks). It then uses `rsvg-convert` to render the vector graphic into a high-quality PNG for the viewport.

### 2. Smart Dependency Checking & "Pro Mode"
* **Automated Fallback:** The IDE now runs a `check_dependencies` scan on startup. If it detects `netlistsvg` and `rsvg-convert` installed on your system, it unlocks the NetlistSVG engine ("Pro Mode"). If you don't have them installed, it smartly falls back to the legacy Graphviz engine automatically so your workflow is never broken.

### 3. Customizable Schematic Themes
* **Visual Upgrades:** The `⚙ Settings` menu has been heavily expanded to include a **Schematic Theme** selector.
* **Themes Available:** * **Standard:** The default light mode.
  * **Dark:** Inverts backgrounds and stroke colors to match the dark code editor and terminal, reducing eye strain.
  * **Blueprint:** Applies a deep-blue background with stark white lines, resembling traditional engineering blueprints (`background-color: #003366`).
* **Live Refresh:** Changing the theme in the settings menu will instantly regenerate and re-render the active schematic on your screen without needing to recompile the project.

### 4. Legacy Graphviz Enhancements
* Even if you don't use the new NetlistSVG engine, the old Graphviz engine has been upgraded. The IDE now uses an internal regex patcher (`patch_graphviz_style`) to inject colors and approximate shapes (like triangles for NOT gates) directly into the Yosys `.dot` output to make legacy viewing significantly better.

---

##  Required Dependencies for "Pro Mode"

To unlock the new IEEE standard logic gate viewer, you must install the following tools in your WSL/Linux environment:

**Node.js & NetlistSVG (Universal):**
```bash
# Install Node.js (via your package manager or NVM)
sudo npm install -g netlistsvg
--
## Setup and Installation

### For Linux (Native) & WSL
Ensure you have the following packages installed based on your distribution.

```bash
sudo dnf update
# Install Python, UI, and Image components
sudo dnf install python3-tkinter python3-pillow-tk
# Install EDA Toolchain
sudo dnf install iverilog gtkwave yosys graphviz
