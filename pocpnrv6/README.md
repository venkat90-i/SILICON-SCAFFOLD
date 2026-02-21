# Silicon scaffold IDE (POC PnR v6)

**Silicon scaffold IDE POC PnR v6** (internally designated as the final **"PEAK!"** build) represents the absolute conclusion of the Proof-of-Concept phase. This version focuses on structural stability and refined error handling to ensure the tool is ready for general use by students and silicon designers.



---

##  Final Enhancements in POC PnR v6

This release locks in the most advanced features of the suite while improving the "self-healing" capabilities of the backend:

### 1. Enhanced "Self-Healing" Schematic Worker
* **Robust Failover:** The `SchematicWorker` has been further refined to handle edge cases where Yosys might fail to generate a DOT file due to complex SystemVerilog syntax.
* **Detailed Debugging:** If both the RTL view and the structural view fail, the IDE now surgically extracts the first 200 characters of the `Yosys Stderr` and pipes them directly to the "DBG" log. This allows developers to instantly identify syntax errors without digging through temporary log files.

### 2. Industry-Standard Layout Direction
* **Standardized Flow:** The schematic rendering engine now explicitly enforces a Left-to-Right (`-Grankdir=LR`) flow using Graphviz.
* **Intuitive Navigation:** By forcing inputs to the left and outputs to the right, the IDE ensures that even the most complex hardware architectures remain readable and follow the natural visual logic used in industrial EDA tools.

### 3. Stabilized Dual-World Architecture
* **Frontend vs. Backend:** The transition between the Logic Design (Frontend) and Physical Design (Backend) worlds is now seamless. 
* **State Preservation:** The IDE successfully maintains your project context (active PDK, current file, and terminal history) when switching between tabs, ensuring your workflow isn't interrupted when moving from Verilog coding to GDSII generation.

### 4. Optimized Silicon Visualizer (HUD 2.1)
* **High-Fidelity Rendering:** The `SiliconPeeker` continues to utilize hardware acceleration via `QOpenGLWidget` to render thousands of physical assets—including standard cells, pins, and power rails—without performance degradation.
* **Dynamic Scale Accuracy:** The floating HUD scale bar remains fully calibrated, providing real-world micron and nanometer measurements that update in real-time as you zoom into the silicon die.



---

