# Silicon scaffold Workbench (POC v9)

**Silicon scaffold Workbench v9** (internally designated as the "Smart Autocomplete" build) brings the IDE closer to a production-ready state. This release heavily upgrades the terminal's path resolution capabilities and introduces standard hardware function-key shortcuts for rapid development.

---

##  What's New in POC v9 (Improvements)

This version replaces experimental features with robust, standard IDE behaviors for file navigation and compilation:

### 1. Smart Nested Tab Auto-Completion
* **Previous Constraint:** Earlier auto-complete implementations (Spacebar or Right Arrow) could only detect files in the immediate root directory. You could not auto-complete a file path if it was inside a folder (e.g., typing `cd src/m` would fail).
* **v9 Improvement:** The IDE officially returns to the industry-standard **Tab Key (`<Tab>`)** for auto-completion, but with a completely rewritten backend.
* **Nested Pathing:** The terminal now intelligently splits your input (`os.path.split`). If you type `cd src/test_` and press Tab, the IDE looks *inside* the `src` directory to complete the path. It automatically appends trailing slashes to directories to speed up deep folder navigation.

### 2. Global Function Key Shortcuts (F-Keys)
* **New Workflow:** You no longer need to use the mouse to run your code or view hardware diagrams. Standardized hardware shortcuts have been mapped globally across the application:
  * **`F1`**: Instantly save, compile, and run the simulation.
  * **`F2`**: Quickly open the latest `.vcd` waveform in GTKWave.
  * **`F3`**: Instantly generate and display the gate-level schematic.
* The top toolbar buttons have been visually updated (e.g., "F1 Compile") to constantly remind users of these fast-action keys.

### 3. Dynamic UI Shortcut Labels
* **Previous Constraint:** If a user changed their Superkey bindings in the Settings menu (e.g., changing the Editor focus from `c` to `e`), the text labels on the window panes still displayed the old hardcoded defaults.
* **v9 Improvement:** A new `update_ui_labels()` engine has been added. Whenever you save changes in the Settings menu, the titles of the four main panes (Explorer, Code, Schematic, Terminal) instantly update to reflect your custom keyboard mappings.
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
