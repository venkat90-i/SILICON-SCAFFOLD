# Silicon scaffold Workbench (POC v5)

**Silicon scaffold Workbench v5** introduces a massive overhaul to the code editing experience. Moving away from a basic text box, this release implements a custom-built, professional-grade code editor tailored specifically for Verilog development, alongside advanced compiler debugging features.

---

##  What's New in POC v5 (Improvements)

This version focuses heavily on text editing quality-of-life and debugging speed compared to previous builds:

### 1. Custom Pro Code Editor
* **Advanced Text Widget:** The standard `ScrolledText` widget has been entirely replaced by a custom `CodeEditor` class. This provides a much stronger foundation for IDE-like features.
* **Dynamic Line Numbers:** A dedicated gutter pane now displays line numbers on the left side of the editor. The line numbers automatically update as you type and stay perfectly synced with your vertical scrolling.

### 2. Real-Time Syntax Highlighting
* **Verilog Keyword Support:** The editor now uses regular expressions to parse and colorize Verilog code dynamically as you type. 
* **Color Scheme:**
  * **Keywords** (`module`, `always`, `wire`, `reg`, etc.) are highlighted in bold blue.
  * **Comments** (`//`) are green.
  * **Strings** are red or orange.
  * **Numbers** (including hex/binary declarations like `8'hFF`) are purple.

### 3. Smart Error Detection & Jumping
* **Automated Debugging:** When you click "Compile & Run" and the `iverilog` compiler encounters a syntax error, the IDE now automatically parses the standard error log for the exact line number where the failure occurred.
* **Visual Error Highlighting:** The editor will automatically scroll to the buggy line and highlight the entire line with a red background so you can fix it immediately without hunting through the file.
---
## 📥 Setup and Installation

### For Linux (Native) & WSL
Ensure you have the following packages installed based on your distribution.

```bash
sudo dnf update
# Install Python, UI, and Image components
sudo dnf install python3-tkinter python3-pillow-tk
# Install EDA Toolchain
sudo dnf install iverilog gtkwave yosys graphviz
