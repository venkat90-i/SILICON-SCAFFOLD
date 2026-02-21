# Silicon scaffold IDE (POC v20)

**Silicon scaffold IDE v20** (internally designated as the "Hierarchy Fix" build) attempts to stabilize the ambitious synthesis and reporting features introduced in recent iterations. This release focuses on replacing fragile text-parsing methods with robust data-handling libraries to prevent the silent crashes that plagued v19.

---

##  KNOWN ISSUES (BRUTAL WARNING)

**This build is still officially marked by the developer as `!!!!!!!!!!bugged!!!!!!!!!!`**. 
* While the silent crashes from v19 have been targeted, the application is still in an experimental state. 
* You may still encounter unexpected behavior during heavy synthesis workloads or complex schematic rendering. Proceed with caution on production designs.

---

##  What's New in POC v20 (Improvements)

This version introduces critical architectural fixes to how the IDE understands and processes your hardware designs compared to v19:

### 1. Robust JSON Integration
* **Previous Constraint:** In v19, the IDE attempted to read complex Yosys area and power reports using brittle Regular Expressions (Regex). When fed large Verilog files with unexpected output formatting, the Regex engine would fail, causing the IDE to silently crash without a traceback.
* **v20 Improvement:** The IDE now natively imports Python's `json` library. By instructing Yosys to output its statistics in a structured JSON format (`stat -json`), the IDE can now safely and reliably parse deep hardware metrics without crashing, regardless of the design's size.

### 2. The "Hierarchy Fix" (Complex Design Support)
* **Previous Constraint:** The previous module-detection algorithms struggled with deep, multi-file Verilog hierarchies (e.g., a CPU module instantiating an ALU, which instantiates an Adder), leading to bugged schematic views or failed synthesis runs.
* **v20 Improvement:** As indicated by the "Hierarchy Fix" build title, the engine that resolves module dependencies and identifies the "Top" module has been patched. This allows the IDE to better understand multi-layered hardware designs, ensuring that the Yosys `hierarchy` commands properly link your sub-modules together before synthesis or schematic generation.

* --
* ##  Setup and Installation

### For Linux (Native) & WSL
Ensure you have the following packages installed based on your distribution.

```bash
sudo dnf update
# Install Python, UI, and Image components
sudo dnf install python3-tkinter python3-pillow-tk
# Install EDA Toolchain
sudo dnf install iverilog gtkwave yosys graphviz
