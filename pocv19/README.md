# Silicon scaffold IDE (POC v19)

**Silicon scaffold IDE v19** (internally designated as the "Stable Core" build) introduces crucial process-management features to handle heavy compiler workloads. However, despite these architectural upgrades, the application suffers from severe instability when handling real-world, large-scale hardware designs.

---

##  CRITICAL KNOWN ISSUES (BRUTAL WARNING)

**This build is highly unstable under heavy loads and contains broken features.** Based on the developer's explicit warnings, be aware of the following:
* **Silent Crashes on Large Designs:** If you attempt to synthesize or generate reports for massive Verilog codebases, the IDE will silently crash and close without warning or error logs.
* **Useless "Hybterm" Feature:** The hybrid terminal functionality implemented in this build is currently considered a useless, non-functional feature.
* **Bugged Schematic View:** The schematic generation pipeline is heavily bugged and may fail to display your hardware visualizations correctly. 
* **Do not use this version for complex or production-grade VLSI projects.**

---

##  What's New in POC v19 (Improvements)

Despite the critical bugs mentioned above, this version introduces major underlying improvements to process handling and UI stability compared to v18:

### 1. Emergency Stop & Job Locking
* **Previous Constraint:** In older versions, if you started a massive simulation or synthesis job, you had to wait for it to finish or force-kill the entire Python IDE through your OS task manager. Clicking "Compile" twice would also spawn overlapping, conflicting threads.
* **v19 Improvement:** A global `is_running_job` lock has been implemented. Once a compile, simulate, or synthesis job starts, the IDE disables the F1, F3, and F4 buttons so you cannot accidentally trigger concurrent builds. 
* **🛑 STOP Button:** A new, dedicated red Emergency Stop button has been added to the top toolbar. Clicking it instantly sends a `kill()` signal to the underlying `iverilog` or `yosys` subprocess, instantly halting runaway jobs and freeing your workspace.

### 2. "Firehose" Terminal Throttling
* **Previous Constraint:** When Yosys outputs thousands of lines of synthesis logs in milliseconds, the standard Tkinter `queue.get()` loop would completely freeze the GUI as it struggled to print every single line.
* **v19 Improvement:** The IDE now uses a "Firehose Valve" throttled update mechanism (`update_log_view`). Instead of printing line-by-line, the IDE reads everything currently in the queue, concatenates it into a single massive text block (`"".join(lines)`), and pushes it to the terminal all at once. It only checks the queue every 50ms (`after(50)`), ensuring your IDE remains smooth and responsive even during heavy compilation.

### 3. Chained Synthesis Execution Thread
* **Advanced Pipeline:** The `F4` Synthesis flow has been completely rewritten into a chained, synchronous background thread (`synth_thread`). 
* **Sequential Flow:** It first runs Yosys, pipes the output to the terminal, automatically extracts the chip area, and then *immediately* triggers the OpenSTA (Static Timing Analysis) tool. Once both heavy processes finish safely in the background, it signals the main GUI to parse the logs and print a clean `[IMPL SUMMARY]` containing your Timing Slack and Total Power metrics.

* --
* ## 📥 Setup and Installation

### For Linux (Native) & WSL
Ensure you have the following packages installed based on your distribution.

```bash
sudo dnf update
# Install Python, UI, and Image components
sudo dnf install python3-tkinter python3-pillow-tk
# Install EDA Toolchain
sudo dnf install iverilog gtkwave yosys graphviz
