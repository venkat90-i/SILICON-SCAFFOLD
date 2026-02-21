# Silicon scaffold IDE (POC PnR v18)

**Silicon scaffold IDE POC PnR v18** (officially branded in the code as **"Silis — Silicon Scaffold v2.1"**) is a massive architectural milestone. Moving away from simply wrapping external terminal tools, this release builds complex, native visualizers directly into the PyQt6 interface, creating a truly unified EDA suite.

---

## What's New in POC PnR v18 (Improvements)

This version entirely overhauls the frontend user experience, introducing native waveform viewing, hardware-accelerated layouts, and professional reporting:

### 1. The Native "SignalPeeker" Waveform Engine
* **Previous Constraint:** Users had to rely completely on external tools like GTKWave to view their `.vcd` simulation results.
* **PnR v18 Improvement:** The IDE now features its own incredibly robust, native `VCDParser` and `WaveformCanvas`. 
* **Features:** It cleanly renders single-bit signals (green/red lines) and multi-bit buses (hexagonal shapes with hex values). It includes keyboard navigation for zooming, panning, and instant edge-jumping (using the `A` and `D` keys to snap to the next signal transition).

### 2. Professional Synthesis Dashboard & Report Engine
* **Previous Constraint:** Parsing Yosys and OpenSTA logs was messy, and users had to manually dig through text to find timing violations or power metrics.
* **PnR v18 Improvement:** The new `SynthesisTab` introduces a beautiful, split-pane dashboard.
* **The `ReportEngine`:** A powerful background class now automatically extracts your total area, gate count, critical timing paths, Worst Negative Slack (WNS), and exact power splits (Leakage vs. Switching). It compiles this data into a stunning, printable ASCII-art "Post Synthesis Report".

### 3. GPU-Accelerated Silicon Peeker & Dynamic HUD
* **The "Breaking Apart" Fix:** To solve rendering artifacts when zooming deeply into massive silicon dies, the `SiliconPeeker` has been upgraded to use a native `QOpenGLWidget` for hardware acceleration, combined with a `FullViewportUpdate` mode to ensure flawless rendering.
* **Dynamic Scale Bar (HUD):** The viewer now features a brilliant red, floating HUD in the bottom right corner. As you zoom in and out, it dynamically calculates the Database Units (DBU) to display an accurate, real-world scale bar transitioning seamlessly between micrometers (µm) and nanometers (nm).

### 4. RTL-Preserving Schematic Engine
* **Previous Constraint:** Synthesizing complex designs often caused the `netlistsvg` engine to explode into an unreadable mess of 10,000 NAND/NOR gates.
* **PnR v18 Improvement:** The Yosys command inside the `SchematicWorker` has been specifically tuned (`proc; opt; show`) to skip the final `techmap` and `abc` passes. This ensures your schematic remains at the clean, high-level RTL block view (Registers, Muxes, Adders) rather than flattening into a sea of standard cells.

### 5. Unified 4-Step Architecture
* **UI Polish:** The IDE now perfectly organizes your workflow into distinct, numbered tabs (`1. COMPILE`, `2. WAVEFORM`, `3. SCHEMATIC`, `4. SYNTHESIS`) allowing you to easily step through the logical design phase before flipping over to the Backend physical layout.
