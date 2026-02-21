# Silicon scaffold Workbench (POC v10)

**Silicon scaffold Workbench v10** (internally designated as the "Pro Terminal" build) drastically improves the debugging experience. This version transforms the standard output console into a smart, color-coded terminal with customizable themes and improved visual layouts.

---

##  What's New in POC v10 (Improvements)

This version brings intelligent output parsing and layout enhancements to the terminal compared to v9:

### 1. Smart Color-Coded Terminal (Auto-Tagging)
* **Previous Constraint:** In v9, all terminal output (errors, successes, warnings, and system logs) was printed in a single monochrome color, making it tedious to hunt down specific Verilog syntax errors.
* **v10 Improvement:** The terminal now features an auto-tagging engine. As the `iverilog` or `vvp` compiler streams output, the IDE intelligently scans the text in real-time. If it detects keywords like "error", "syntax", or "warning", it dynamically applies specific color tags (e.g., Red for errors, Yellow for warnings). This makes critical compiler feedback pop out immediately.

### 2. Customizable Terminal Themes
* **Personalized UX:** The `⚙ Settings` menu has been expanded to include a "Terminal Colors" configuration section. You can now define custom Hex color codes for five distinct terminal states: `SYS`, `INPUT`, `ERROR`, `SUCCESS`, and `WARN`.
* **Live Updates:** Changes are saved and applied instantly across the entire terminal history via the `update_term_colors()` function without needing to restart the IDE.

### 3. Grid-Aligned Auto-Completion
* **Previous Constraint:** When pressing `<Tab>` in v9 with multiple matching files (ambiguous matches), the terminal would simply print a basic comma-separated list of the options.
* **v10 Improvement:** The IDE now implements a `print_grid` function. It dynamically calculates the length of the longest file name and formats the autocomplete options into neatly aligned, spaced columns (similar to how the native Linux `ls` command behaves). This keeps the terminal clean and highly readable.
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
