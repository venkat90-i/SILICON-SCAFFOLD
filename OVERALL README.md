#  Silis IDE: Complete Version Evolution & Comparative Changelog

Silis has undergone a massive architectural evolution. To understand the engineering behind the IDE, below is the detailed, version-by-version breakdown of our development journey. Each milestone details the previous limitations, the features added, and the comparative improvements made to stability and architecture.



---

##  Phase 1: The `popcv` RTL Foundation (v1 to Pnrv5)

### `v1`: The IDE Genesis
* **Previous State:** No unified workspace; developers relied on separate command-line execution for editing, simulation, and synthesis.
* **Improvement & Additions:** Birthed the main IDE window and `Editor` class. Integrated a Verilog editor with basic subprocess handling to hook into Icarus Verilog and Yosys.
* **Architectural Impact:** Established the foundational RTL IDE structure, allowing code and compilation to exist in one window.

### `v2 - v5`: Waveform & Debug Integration
*(Iterative hardening across 4 versions)*
* **Previous State (v1):** Users had to manually locate and open VCD files in external viewers; simulation errors were difficult to trace.
* **Improvement & Additions:** Introduced waveform integration classes with direct GTKWave integration and native VCD support. 
* **Comparative Improvement:** Iteratively improved compile log routing. Instead of silent failures, simulation errors and waveform outputs were heavily integrated, adding a true debugging capability to the IDE.

### `v6 - v10`: Project Explorer & Workspace Structuring
*(Iterative hardening across 5 versions)*
* **Previous State (v5):** Flat file management relying on standard OS dialogs, making multi-module Verilog projects hard to manage.
* **Improvement & Additions:** Built the `Project Explorer` class, introducing file tree navigation and improved open/save mechanics.
* **Comparative Improvement:** Shifted from basic file tracking to advanced file state tracking, resulting in a structured, professional IDE layout that persists user workspaces.

### `v11 - v15`: Threaded RTL Schematic Extraction
*(Iterative hardening across 5 versions)*
* **Previous State (v10):** Abstract Verilog code could not be visually verified without running heavy external logic synthesizers, which often froze the GUI.
* **Improvement & Additions:** Added the `Schematic Worker` class to generate visual RTL schematics natively using `yosys show`.
* **Comparative Improvement:** Implemented threaded execution. Compared to earlier builds, the IDE now prevents UI freezing during heavy logic extraction, introducing robust RTL visualization support.

### `v16 - v20`: Synthesis Dashboard & Analytics
*(Iterative hardening across 5 versions)*
* **Previous State (v15):** Synthesis generated massive, chaotic text logs that were difficult for beginners to parse for critical data (like cell counts).
* **Improvement & Additions:** Deployed a centralized `Dashboard` class featuring synthesis output previews and direct metric displays.
* **Comparative Improvement:** Separated compilation logs by tabs. The architecture moved from raw text dumping to a highly structured synthesis interface.

### `v21 - v23`: Professional Waveform Engine
*(Major iterative hardening across 10 versions)*
* **Previous State (v21):** The basic VCD implementation was prone to crashing when handling massive simulation dumps from complex designs.
* **Improvement & Additions:** Massively upgraded the `VCDParser` to include bus waveform rendering and edge-to-edge navigation.
* **Comparative Improvement:** Added critical crash-proof parsing safeguards. This transformed the IDE's simulation analysis from a basic viewer into a professional, industrial-grade waveform debugging environment.



### `v24 - v26`: Automated Constraints & Beginner-Safe Timing
*(Iterative hardening across 5 versions)*
* **Previous State (v23):** Static Timing Analysis (STA) tools would frequently crash or fail entirely if users (especially beginners) forgot to write complex SDC constraint files.
* **Improvement & Additions:** Implemented Auto SDC generation logic, which automatically applies baseline clock and delay constraints.
* **Comparative Improvement:** Completely prevents STA crashes for unconstrained designs, creating a "beginner-safe" timing flow that didn't exist before.

### `pnrv1 - pnrv5`: Frontend UX Maturation
*(Iterative hardening across 4 versions)*
* **Previous State (v1):** The workflow was functional but clunky, requiring too many mouse clicks to navigate between editing, simulation, and logs.
* **Improvement & Additions:** Polished the frontend UX with global F-key shortcuts and improved keyboard navigation.
* **Comparative Improvement:** Finalized log routing cleanup. This marked the official maturation of the RTL world (`popcv`), ensuring it was perfectly stable before the massive architectural expansion into backend design.

---

##  Phase 2: The `pocpnrv` Physical Design Leap (pnrv1 to pnrv3)

### `v40`: Birth of the Physical World
* **Previous State (v1):** Silis was purely an RTL tool with zero physical layout awareness.
* **Improvement & Additions:** Introduced the `DEFParser` and `SiliconPeeker` classes, establishing a physical layout viewer that renders nets and a basic heatmap.
* **Comparative Improvement:** Achieved $O(1)$ component lookup, allowing the GUI to render physical layouts without the heavy lag typical of Python-based EDA viewers.

### `pnrv1 - pnrv2`: State-Machine Parser & Organic Heatmaps
* **Previous State (v1):** The initial DEF parser was brittle and lacked power infrastructure visibility.
* **Improvement & Additions:** Completely rewrote the DEF parser using a state-machine architecture. Added power rail parsing and organic heatmaps.
* **Comparative Improvement:** Safer, more resilient parsing logic transformed the basic viewer into a professional layout visualization tool.

### `pnrv2 - pnrv3`: Technology Awareness (`PDKManager`)
*(Iterative hardening across 3 versions)*
* **Previous State (v1):** Physical dimensions and rules were hardcoded or heavily assumed.
* **Improvement & Additions:** Integrated the `PDKManager` class, introducing multi-PDK selection (e.g., Skywater 130nm) and robust config loading.
* **Comparative Improvement:** Added a persistent cache. The backend is now fully "technology-aware," adapting its rules based on the selected foundry PDK.

### `pnrv4 `: Engineering Report Engine
*(Iterative hardening across 4 versions)*
* **Previous State (v3):** OpenROAD backend metrics were buried deep in raw console outputs.
* **Improvement & Additions:** Built a structured `ReportEngine` implementation to specifically extract power, timing, and cell utilization reports.
* **Comparative Improvement:** Safer log parsing abstracts away backend chaos, creating an engineering-grade reporting system directly in the IDE.


### `pnrv5`: GPU-Accelerated Z-Layer Rendering
* **Previous State (v4):** Layouts were rendered flat, making it impossible to distinguish between overlapping metal layers, pins, and power rails visually.
* **Improvement & Additions:** Formalized a complete Z-layer model for layered rendering (die area, power nets, signal routing, pins, heatmaps).
* **Comparative Improvement:** Implemented stable GPU viewport handling. The layout engine is now structured, allowing users to independently toggle specific physical layers.



