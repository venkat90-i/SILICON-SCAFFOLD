# Silicon scaffold IDE (POC PnR v1)

**Silicon scaffold IDE POC PnR v1** (internally designated as the "PDK Manager" build) marks the most significant evolutionary milestone since the project's inception. Having perfected the "Frontend" (RTL Simulation and Logic Synthesis), this release officially introduces the **Backend Physical Design (Place and Route)** pipeline. 

The IDE has evolved into a full RTL-to-GDSII suite, capable of taking your synthesized netlist and physically laying it out onto a silicon floorplan.

---

##  What's New in POC PnR v1 (Improvements)

This release fundamentally changes the architecture of the IDE, splitting the workflow into two distinct engineering phases:

### 1. Dual-Tab Architecture (Frontend vs. Backend)
* **Previous Constraint:** All operations (editing, terminal, schematics) were crammed into a single view.
* **PnR v1 Improvement:** The entire application is now wrapped in a native `QTabWidget`.
  * **Tab 1: Frontend (Logic):** Contains the familiar Code Editor, Explorer, and SVG Schematic Viewer for RTL development and Logic Synthesis.
  * **Tab 2: Backend (Physical):** A completely new interface dedicated to physical chip layout, routing, and GDSII generation.

### 2. Smart PDK "Triangulation Engine"
* **Previous Constraint:** In earlier versions, users had to manually type or browse for a single `.lib` file, which was highly prone to error and insufficient for physical design.
* **PnR v1 Improvement:** The IDE now features a `PDKManager` that automatically scans your hard drive for valid EDA development kits.
* **The "Triangulation" Check:** To register a valid PDK, the scanner strictly mandates that three components must exist in the directory tree: a Timing file (`.lib`), a Cell Shape file (`.lef`), and a Tech Layer file (`.tlef`). If it finds all three, it binds them into a profile and caches them.
* **Interactive Selector:** A new `PDKSelector` GUI lets you filter, search, and visually verify your PDK configurations before initiating the physical build.

### 3. OpenROAD Integration & PnR Ribbon
* **Physical Synthesis Begins:** The Backend tab introduces an interactive `QProcess` wrapper around **OpenROAD**, the industry-standard open-source physical design tool.
* **The 7-Step Pipeline:** A top UI ribbon breaks the complex PnR process down into clickable, sequential steps:
  1. **Init:** Automatically writes and executes an `init_pdk.tcl` script to link your Netlist, LEF, and LIB files.
  2. **Floorplan:** Defines the core dimensions and utilization.
  3. **Tap/Endcap:** Inserts substrate taps.
  4. **Place:** Performs global and detailed cell placement.
  5. **CTS:** Synthesizes the Clock Tree.
  6. **Route:** Performs detailed metal routing.
  7. **GDS:** Exports the final physical `design.gds` file.
* **Live TCL Console:** A dedicated interactive console allows power-users to type raw TCL commands directly into the active OpenROAD backend process.

### 4. The "Silicon Peeker" Visualizer
* **Physical Visualization:** To complement the logic schematic in the Frontend, the Backend features the `SiliconPeeker` (a modified `QGraphicsView`).
* Currently, when you click "Floorplan" or "Place", it generates an auto-scaling, mock visual representation (a density heatmap) of your silicon die. This lays the graphical foundation for rendering actual routed metal layers in future updates.
