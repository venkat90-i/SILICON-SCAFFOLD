# Silicon scaffold IDE (POC v12)

**Silicon scaffold IDE v12** (internally designated as the "Cursor Fixed" build) focuses on polishing the user experience and resolving critical hardware-specific UI bugs common in Linux/WSL environments. 

---

## What's New in POC v12 (Improvements)

This version introduces several quality-of-life enhancements and deepens the schematic engine's visual capabilities compared to v11:

### 1. The "Invisible Cursor" Fix & UI Indicators
* **Previous Constraint:** In earlier versions, pressing the Superkey (Leader Key) changed the mouse cursor into a "crosshair". However, on many WSLg and X-Server setups, this caused the mouse cursor to become permanently invisible, forcing a restart of the IDE.
* **v12 Improvement:** The cursor-changing logic has been completely removed. Instead, the IDE now uses a dedicated **SK Status Indicator** in the top toolbar. When you press the Superkey (`grave`/backtick), the indicator flashes bright green (`SK ACTIVE`) to let you know the IDE is listening for a shortcut, keeping your mouse cursor safe and visible.

### 2. Context Menus & File Deletion
* **File Management:** You no longer need to use the terminal to delete files. The Project Explorer now supports a Right-Click context menu (`<Button-3>`). 
* **Safety First:** Clicking "Delete" (or pressing the `<Delete>` key on your keyboard while selecting a file) triggers a confirmation dialog (`messagebox.askyesno`) before safely removing the file or directory using Python's `shutil` and `os` libraries.

### 3. Standard Global Keyboard Shortcuts
* **Accessibility:** While the Superkey workflow is great for power users, v12 introduces standard OS-level shortcuts for immediate convenience:
  * **`Ctrl + S`**: Instantly saves the current file.
  * **`Ctrl + N`**: Creates a new, blank file.

### 4. Advanced SVG CSS Injection (True Theming)
* **Previous Constraint:** In v11, the Dark and Blueprint themes for the new NetlistSVG engine were applied using a basic string replacement hack, which sometimes failed to color the logic gates properly.
* **v12 Improvement:** The IDE now features a robust `inject_svg_css` function. When generating a schematic, it dynamically writes and injects a standard HTML/CSS `<style>` block directly into the SVG file before converting it to a PNG. This ensures that every wire, pin, and IEEE logic gate perfectly inherits the high-contrast white strokes required for the Dark and Blueprint themes.

---
### For Linux (Native) & WSL
Ensure you have the following packages installed based on your distribution.

```bash
sudo dnf update
# Install Python, UI, and Image components
sudo dnf install python3-tkinter python3-pillow-tk
# Install EDA Toolchain
sudo dnf install iverilog gtkwave yosys graphviz
