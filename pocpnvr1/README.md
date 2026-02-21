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

<div class="silis-table-container">
    <table class="silis-tools-table">
        <thead>
            <tr>
                <th>Category</th>
                <th>Tool / Library</th>
                <th>Primary Purpose in Silis IDE</th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td><strong>Framework & GUI</strong></td>
                <td><span class="highlight">PyQt6</span></td>
                <td>Core interface, rendering the Silicon Peeker, and managing background processes.</td>
            </tr>
            <tr>
                <td><strong>Logic Simulation</strong></td>
                <td><span class="highlight">Icarus Verilog & VVP</span></td>
                <td>Compiling and running standard Verilog and SystemVerilog code.</td>
            </tr>
            <tr>
                <td><strong>Waveform Viewer</strong></td>
                <td><span class="highlight">GTKWave</span></td>
                <td>Visualizing the <code>.vcd</code> waveform output from the simulation phase.</td>
            </tr>
            <tr>
                <td><strong>Logic Synthesis</strong></td>
                <td><span class="highlight">Yosys</span></td>
                <td>Mapping behavioral RTL code into structural gate-level netlists.</td>
            </tr>
            <tr>
                <td><strong>Timing Analysis</strong></td>
                <td><span class="highlight">OpenSTA</span></td>
                <td>Extracting hardware timing constraints, power, and area reports.</td>
            </tr>
            <tr>
                <td><strong>Schematic Engine</strong></td>
                <td><span class="highlight">NetlistSVG & Graphviz</span></td>
                <td>Rendering high-resolution, vector-based hardware logic diagrams.</td>
            </tr>
            <tr>
                <td><strong>Physical Design</strong></td>
                <td><span class="highlight">OpenROAD</span></td>
                <td>Driving the entire backend Place and Route (PnR) flow to generate a physical chip layout.</td>
            </tr>
            <tr>
                <td><strong>Data Parsing</strong></td>
                <td><span class="highlight">JSON & XML</span></td>
                <td>Managing the PDK configuration cache and surgically patching SVG visual styles.</td>
            </tr>
        </tbody>
    </table>
</div>


