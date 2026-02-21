# Silicon scaffold Workbench (POC v7)

**Silicon scaffold Workbench v7** (designated in the code as the v8.1 Fixed Syntax build) focuses on refining the user experience. This release enhances accessibility by adding full keyboard support to the visualizer and replaces experimental terminal features with industry-standard, shell-like behaviors.

---

##  What's New in POC v7 (Improvements)

This version brings precise keyboard controls to the schematic engine and upgrades the terminal's auto-completion logic to prevent typing interference:

### 1. Keyboard-Driven Schematic Navigation
* **Previous Constraint:** Navigating large, generated hardware schematics required clicking, dragging, and using the mouse scroll wheel. This interrupted the keyboard-centric workflow introduced in v6.
* **v7 Improvement:** The `ZoomableSchematic` viewer now fully supports direct keyboard navigation. 
  * **Focus:** Clicking once on the canvas now explicitly grants it keyboard focus.
  * **Panning:** You can use the standard **Arrow Keys** (Up, Down, Left, Right) or their Numpad equivalents to smoothly pan around complex logic diagrams.
  * **Zooming:** Use the **`+`** (Plus/Add) and **`-`** (Minus/Subtract) keys to zoom in and out of the schematic without needing a mouse wheel.

### 2. "Fish-Shell" Style Right-Arrow Auto-Completion
* **Previous Constraint:** The "Spacebar Auto-Complete" introduced in v6 was innovative but flawed; it often interfered with typing normal spaces when writing standard, multi-word shell commands (like `iverilog -o design.out`).
* **v7 Improvement:** The spacebar hack has been completely removed. It is replaced with a much smarter **Right Arrow (`<Right>`)** auto-completion system, heavily inspired by modern terminals like Fish or Zsh.
* **How it works:** When typing in `[SHELL]` mode, pressing the Right Arrow key evaluates your current directory for a matching file or folder prefix. Crucially, the IDE now calculates your cursor's exact position; it *only* triggers the auto-complete if your cursor is at the absolute end of the input line. This ensures that using the arrow keys to edit the middle of a command works perfectly without accidentally triggering file completions.

* ---
* ### For Linux (Native) & WSL
Ensure you have the following packages installed based on your distribution.

```bash
sudo dnf update
# Install Python, UI, and Image components
sudo dnf install python3-tkinter python3-pillow-tk
# Install EDA Toolchain
sudo dnf install iverilog gtkwave yosys graphviz
