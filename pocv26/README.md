# Silicon scaffold IDE (POC v34)

**Silicon scaffold IDE v34** (internally designated as the "Uncapped" v3.9.1 build) tackles the final performance bottleneck of the IDE. This release ensures that generating incredibly large, complex ASIC schematics never freezes the application, and it removes the artificial safety limiters from previous versions to allow for truly massive hardware compilation.

---

##  What's New in POC v34 (Improvements)

This release entirely restructures how the IDE handles heavy visual rendering compared to v25:

### 1. Asynchronous Schematic Rendering (QThread)
* **Previous Constraint:** Even though the PyQt6 UI was fast, clicking "F3 Schem" would still freeze the IDE for several seconds (or longer) while Yosys and NetlistSVG computed the diagram synchronously in the main loop.
* **v34 Improvement:** Schematic generation has been completely moved into a background thread via the new `SchematicWorker(QThread)` class. 
* **Seamless Workflow:** When you generate a schematic, the IDE immediately returns control to you. You can continue typing code or interacting with the terminal while the vector graphic compiles silently in the background. Once finished, the worker uses PyQt signals (`pyqtSignal`) to safely pass the SVG back to the main thread and pop it onto your canvas.

### 2. "Uncapped" Engine Limits (8GB RAM)
* **Previous Constraint:** In v25, `netlistsvg` was capped at 4GB of RAM and had a strict 15-second timeout, which often caused massive designs to fail and gracefully downgrade to the Graphviz engine.
* **v34 Improvement:** As the "Uncapped" title suggests, the training wheels are off.
  * The Node.js memory limit (`--max-old-space-size`) has been explicitly doubled from 4096 to **8192 (8GB of RAM)** to support colossal JSON netlists.
  * The `timeout=15` parameter has been entirely removed (`# NO TIMEOUT`). Because the generation is now safely threaded, the IDE allows the compiler to take exactly as long as it needs to process gigabytes of hardware logic without timing out.

### 3. Silent Execution Logs
* **Terminal Polish:** To prevent the background schematic thread from spamming your active simulation or synthesis logs, the `SchematicWorker` now intentionally routes all Yosys and NetlistSVG system outputs to `subprocess.DEVNULL`. This keeps your dashboard perfectly clean, only emitting a single "Generating Schematic..." message when starting.
