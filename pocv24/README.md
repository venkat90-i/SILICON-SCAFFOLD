# Silicon scaffold  IDE (POC v24)

**Silicon scaffold IDE v24** (internally designated as the "Context File Manager" build) completes the massive transition to the PyQt6 framework by restoring and heavily upgrading the advanced workspace management features that were temporarily left behind during the UI rewrite. 

---

##  What's New in POC v24 (Improvements)

This release focuses on feature parity with the final Tkinter builds (v22), bringing back the intelligent project organizer and the professional IEEE schematic engine, but executing them much more cleanly in PyQt6:

### 1. Surgical Workspace Organizer Restored
* **Previous Constraint:** In the initial PyQt6 port (v23), the IDE stopped automatically organizing files into project folders, falling back to a messy root directory.
* **v24 Improvement:** The "Auto-Organizer" logic has been officially ported and stabilized (`prep_workspace`). 
* **Smart Context Tracking:** When you click Compile or Synthesize, the IDE now automatically creates standard ASIC directories (`source/`, `netlist/`, `reports/`) and surgically moves your design files and testbenches into them using `shutil`. Crucially, if it moves the file you currently have open in the editor, it instantly updates the active file path and window title, ensuring you never lose your context.

### 2. NetlistSVG Engine with Native XML Patching
* **Previous Constraint:** v23 only supported basic Graphviz bubbles for schematics. The old Tkinter method of styling NetlistSVG relied on a hacky CSS string-injection that didn't always render properly.
* **v24 Improvement:** The beautiful, IEEE-standard logic gate viewer (NetlistSVG) has been restored. 
* **Advanced SVG Parsing:** To ensure perfect rendering in the new `QGraphicsScene` viewer, the IDE now uses Python's native `xml.etree.ElementTree` library (`patch_netlist_svg`). It surgically iterates through the generated SVG's XML nodes (paths, lines, polygons, text), strips out conflicting inline styles, and enforces clean strokes and fills. This makes the high-resolution vector schematics look stunning.

### 3. Explorer File Deletion
* **Workflow Upgrade:** The native PyQt6 Project Explorer (`SilisExplorer`) has been upgraded to support direct file and folder deletion.
* **Safety First:** Pressing the `Delete` key while highlighting a file triggers a native `QMessageBox.question` dialog to confirm you actually want to delete the file before executing `shutil.rmtree` or `os.remove`.

### 4. Schematic Engine Selector
* **UI Polish:** The `⚙ Settings` menu has been restored to its full functionality. It now includes a native `QComboBox` allowing you to seamlessly switch the Schematic Engine between `Auto`, `Graphviz`, and `NetlistSVG`.
