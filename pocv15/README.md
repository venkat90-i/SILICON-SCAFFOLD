# Silicon scaffold IDE (POC v15)

**Silicon scaffold IDE v15** (internally designated as the "Standard Edition" build) focuses heavily on polishing the code editing experience and refining file management operations. This update resolves long-standing text manipulation bugs and adds intelligent typing assistance tailored for Verilog HDL.

---

##  What's New in POC v15 (Improvements)

This release significantly upgrades the `CodeEditor` class and the Explorer context menus compared to v14:

### 1. Smart Verilog Auto-Indentation
* **Previous Constraint:** Pressing `<Return>` in earlier versions simply dropped the cursor to the beginning of the next line, forcing the user to manually hit `Tab` repeatedly to maintain code block structures.
* **v15 Improvement:** The editor now features a context-aware `auto_indent` engine. 
* **How it works:** When you press Enter, the IDE reads the previous line, calculates its exact whitespace, and automatically mirrors that indentation on the new line. Furthermore, if the previous line ends with a block-initiating keyword like `begin`, `module`, `case`, or `)`, it intelligently adds an additional 4 spaces (one standard tab) to the new line automatically.

### 2. Robust Undo/Redo Engine & Dedicated Toolbar
* **Previous Constraint:** The default Tkinter `undo=True` implementation was notoriously buggy; pressing `<Ctrl-Z>` often deleted the entire document instead of just the last typed word.
* **v15 Improvement:** The undo/redo stack has been completely rebuilt using `autoseparators=True` and manual `edit_separator()` injection triggers on every keystroke. This ensures that "Undo" steps back exactly one action at a time, exactly as expected in a modern IDE.
* **New UI:** A dedicated mini-toolbar has been added directly to the top of the Code Editor pane featuring clickable `↶` (Undo) and `↷` (Redo) buttons. The standard `<Control-z>` and `<Control-y>` shortcuts are now strictly bound to the text area to prevent accidental triggers.

### 3. File Renaming via Context Menu
* **Previous Constraint:** Users could delete files via the right-click context menu, but if they made a typo in a filename, they had to use the terminal to run a `mv` command.
* **v15 Improvement:** The Project Explorer's right-click context menu has been expanded to include a **"Rename"** option. Clicking this opens a standard dialog box prompting for the new name. If you rename the file you currently have open in the editor, the IDE smartly updates your active workspace and window title so your work is never interrupted.
* ---
* ##  Setup and Installation

### For Linux (Native) & WSL
Ensure you have the following packages installed based on your distribution.

```bash
sudo dnf update
# Install Python, UI, and Image components
sudo dnf install python3-tkinter python3-pillow-tk
# Install EDA Toolchain
sudo dnf install iverilog gtkwave yosys graphviz. 
