# Silicon scaffold IDE (POC PnR v2)

**Silis IDE POC PnR v2** (internally designated as the "Silicon Visualizer" build) dramatically enhances the backend physical design experience. While PnR v1 introduced the capability to run OpenROAD, this version gives you the ability to actually *see* the physical silicon structures you are building directly inside the IDE.

---

##  What's New in POC PnR v2 (Improvements)

This release upgrades the IDE's backend from a simple command-line wrapper into a highly interactive physical design viewer:

### 1. Robust DEF Parser & True Silicon Rendering
* **Previous Constraint:** In PnR v1, the "Silicon Peeker" was a mock visualizer that just drew an auto-scaling heatmap box. 
* **PnR v2 Improvement:** The IDE now features a fully custom Python `DEFParser`. When OpenROAD completes a step (like Floorplan or Place), the IDE saves a temporary Design Exchange Format (`temp.def`) file and parses it line-by-line.
* **Detailed Graphics:** The `SiliconPeeker` uses this parsed data to natively render the exact dimensions of your silicon layout using `QGraphicsScene`. It precisely plots the Die Area, Standard Cells (blue), Tap Cells (light purple), Power Rails (orange), and IO Pins (red triangles). 

### 2. Interactive Layer Controls & Overlay Dashboard
* **Visual Filtering:** The backend sidebar now includes a "**Layers**" toggle dashboard. You can check/uncheck boxes to hide or show specific physical layers (Cells, Pins, Nets, Power) on the fly to declutter dense silicon layouts.
* **Organic Heatmap Mode:** A dedicated "Heatmap" toggle button renders your design's density organically. It uses highly translucent red shapes (`QColor(255, 0, 0, 8)`) expanded around every standard cell to visually highlight dense routing congestion areas on your chip.

### 3. Manual PDK Override (Custom Technology Nodes)
* **Previous Constraint:** The v1 Triangulation scanner was powerful, but if you had a non-standard or proprietary PDK folder structure, the IDE would refuse to load it.
* **PnR v2 Improvement:** The PDK Selector now features a bold red "**Pick Custom...**" button. This opens a `ManualPDKDialog` that bypasses the scanner entirely, allowing you to explicitly browse and assign your own custom Tech LEF, Macro LEF, and Liberty (`.lib`) files to build a bespoke technology profile.

### 4. The "Native GUI" Bridge
* **Professional Debugging:** Sometimes, the custom PyQt `SiliconPeeker` isn't enough for deep physical verification. 
* **PnR v2 Improvement:** A **"Native GUI"** button has been added to the backend sidebar. Clicking this automatically generates a `view.tcl` script linking your current PDK and layout files, and then instantly launches the heavy, native C++ OpenROAD graphical interface (`openroad -gui`) for advanced industrial debugging.
