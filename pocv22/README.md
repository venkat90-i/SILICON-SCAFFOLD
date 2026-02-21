# Silicon scaffold IDE (POC v22)

**Silicon scaffold IDE v22** (internally designated as the "Anti-Freeze" v54 build) arrives at a fascinating intersection of major triumphs and new bottlenecks. While the core hardware implementation pipeline is now rock-solid, the IDE struggles under the sheer weight of rendering massive visual assets.

---

##  CRITICAL KNOWN ISSUE: SCHEMATIC CRASHES

**Be warned: The developer explicitly notes this build "CRASHES WITH BIGGER PNG AND SCHEMATICS"**. 
* **The Cause:** In this build, the `generate_schematic` function executes Yosys, NetlistSVG, and Graphviz synchronously via `subprocess.run`. This blocks the Tkinter main loop. 
* **The Result:** When processing large Verilog designs, generating and loading a massive high-resolution schematic takes too long, causing the OS to freeze the application and eventually crash out of memory when trying to load the giant PNG into the canvas. 

---

##  What's New in POC v22 (Improvements)

Despite the schematic viewer issues, this release completely masters the ASIC compilation backend and introduces advanced error-tracking UI features:

### 1. Flawless SDC & Synthesis Pipeline
* **Major Milestone:** The developer officially marks the ASIC backend as **"WORKS FLAWLESSLY WITH SDC FILE ISSUES"**. 
* **Stable Core:** The experimental routing of the `F4` command to generate Synopsys Design Constraints, map to the PDK, and extract Area/Power/Timing metrics via OpenSTA is now fully functional and stable. 

### 2. The "Violation Window" Dashboard
* **Previous Constraint:** Earlier versions dumped thousands of lines of Yosys and OpenSTA logs into a single terminal, making it impossible to find critical timing violations or synthesis warnings.
* **v22 Improvement:** The bottom terminal pane has been upgraded into a dual-screen **Dashboard**. 
  * **Left Side:** The standard system log and shell terminal.
  * **Right Side:** A dedicated, dark-red **"Violation Window"** specifically for Errors and Warnings.

### 3. The Log Harvester & "Panic Button"
* **Automated Auditing:** The IDE now features a `harvest_logs` engine. After synthesis completes, it silently reads through `synthesis.log` and `sta.log`.
* **Smart Filtering:** It filters out the noise and surgically extracts only the lines containing "Error" or "Warning", piping them directly into the Violation Window.
* **UI Indicator:** A new **"⚠️ Show Errors"** button sits on the top toolbar. It remains disabled (grayed out) during normal operation, but actively lights up if the Harvester detects structural violations in your hardware design.

* --
* 
