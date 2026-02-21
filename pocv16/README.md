# Silicon scaffold IDE (POC v16)

**Silicon scaffold IDE v16** (internally designated as the "Anti-Recursion" build) resolves a critical logical flaw in the Auto-Organizer and introduces browser-style directory navigation to the Project Explorer.

---

##  What's New in POC v16 (Improvements)

This release focuses on preventing workspace corruption and speeding up file tree navigation compared to v15:

### 1. Smart Anti-Recursion (The "Inception" Bug Fix)
* **Previous Constraint:** In v14 and v15, the Auto-Organizer was too aggressive. If you navigated *inside* an already-generated project folder (e.g., `alu_project/`) and clicked "Compile" again, the IDE would create a nested folder inside it (e.g., `alu_project/alu_project/`) and move the files deeper, creating an endless Russian-doll directory structure.
* **v16 Improvement:** The `ensure_project_folder` engine now features a strict **Recursion Check**. Before creating a folder or moving files, the IDE analyzes your Current Working Directory (CWD). If it detects that you are already inside the target project folder, it safely aborts the moving process and compiles your code perfectly in place.

### 2. Directory Navigation History (Back & Forward)
* **Previous Constraint:** Navigating deep into complex VLSI project structures was tedious. If you accidentally clicked the wrong folder or went up a directory, you had to manually click your way back through the tree.
* **v16 Improvement:** The IDE now implements a `dir_history` tracking array and a `history_index` pointer. Every time you change directories, the IDE silently records your path. 
* **Scoped Shortcuts:** When you have the Explorer pane selected, you can now use standard undo/redo shortcuts as browser-style navigation:
  * **`<Control-z>`**: Triggers `nav_back()`, instantly returning you to your previously viewed directory.
  * **`<Control-y>`**: Triggers `nav_forward()`, moving you forward in your directory history.

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
