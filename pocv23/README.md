# Silicon scaffold IDE (POC v23)

**Silicon scaffold IDE v23** (internally designated as the "Vector Engine" build) represents the most dramatic architectural shift in the project's history. The developer has officially marked this as the **"LATEST STABLE VERSION"** that **"WORKS FLAWLESSLY"**. 

To solve the fatal out-of-memory (OOM) crashes caused by massive PNG schematics in v22, the entire Integrated Development Environment has been rewritten from the ground up using a professional-grade UI framework.

---

## critical issues 
functions don't work 

##  What's New in POC v23 (Improvements)

This release entirely abandons Tkinter in favor of **PyQt6**, delivering massive performance gains and solving the schematic crashing bug:

### 1. Complete PyQt6 GUI Overhaul
* **Previous Constraint:** Tkinter's single-threaded nature and rudimentary widget set struggled to handle rapid terminal updates, asynchronous file management, and complex text manipulation concurrently.
* **v23 Improvement:** The UI has been completely rebuilt using `PyQt6`. 
  * The Project Explorer now uses a native `QFileSystemModel` for instant, OS-level directory syncing without manual refresh hacks.
  * The window panes are now managed by `QSplitter`, allowing you to smoothly click-and-drag to resize the Code, Schematic, and Terminal areas.

### 2. Vector-Based Schematic Viewer (SVG Engine)
* **The Crash Fix:** To solve the memory crashes from loading giant PNG images, the IDE now utilizes a `SilisSchematic` viewer built on `QGraphicsScene` and `QGraphicsSvgItem`.
* **How it works:** Instead of converting the `.dot` file into a pixel-based PNG, the IDE converts it directly into a scalable `.svg` (Vector Graphic) (`dot -Tsvg`). This allows for infinite, hardware-accelerated zooming without consuming massive amounts of RAM. *(Note: Only the Graphviz engine is active in this specific build).*

### 3. Allocation Limit Safety Removed
* **Massive Design Support:** To ensure the IDE can open ridiculously large generated hardware diagrams, the application explicitly disables Qt's image allocation limit on startup (`QImageReader.setAllocationLimit(0)`). This acts as a "safety off" switch, allowing the UI to render the largest possible silicon schematics.

### 4. Advanced Native Code Editor
* **Previous Constraint:** The Tkinter code editor relied on a hacky "gutter" text box that had to be manually synced to the main text area's scrollbar, which often lagged.
* **v23 Improvement:** The new `CodeEditor` inherits directly from `QPlainTextEdit`. It features a dynamically painted `LineNumberArea` that is natively tied to the editor's block count, ensuring butter-smooth scrolling and perfect line-number alignment. It also automatically highlights the current line your cursor is on in a subtle yellow for better readability.

### 5. Rich HTML Terminal
* **Visual Polish:** The terminal logs no longer rely on Tkinter color tags. The `QTextEdit` terminal now processes and prints raw HTML (`<span style="color:#00FFFF;">`), allowing for much cleaner, highly customizable color-coded system logs.
