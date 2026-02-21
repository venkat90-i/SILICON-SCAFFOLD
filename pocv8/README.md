# Silicon scaffold Workbench (POC v8)

**Silicon scaffold Workbench v8** (internally designated as the "Leak Fix" build) focuses on perfecting the keyboard-centric workflow introduced in previous versions. This release resolves critical event-handling bugs and vastly improves file navigation without needing a mouse.

---

##  What's New in POC v8 (Improvements)

This version introduces robust event interception and expands keyboard controls across the entire IDE:

### 1. "Superkey" Event Leak Prevention
* **Previous Constraint:** When the text editor or terminal had focus, pressing the leader key (now renamed to the **Superkey** or **SK**) would sometimes accidentally type a backtick (\`) into the code or fail to intercept the shortcut commands properly.
* **v8 Improvement:** The IDE now binds the Superkey directly to the `Text` and `Entry` widgets to intercept keystrokes at the widget level. If the Superkey mode is active, the custom `handle_widget_key_intercept` function swallows the next keystroke by returning `"break"`, completely preventing the character from leaking into your Verilog code or terminal.

### 2. Advanced Project Explorer Navigation
The File Explorer (`Treeview`) has been upgraded to support full keyboard traversal:


* **Auto-Focus:** When you switch focus to the Explorer (via `` ` + v ``), it automatically selects the first item in the list so you can immediately start navigating.
* **Enter to Dive:** Pressing `<Return>` on a folder automatically changes the Current Working Directory (CWD) to that folder and toggles its expanded/collapsed state. Pressing `<Return>` on a file opens it in the editor.
* **Escape to Surface:** Pressing `<Escape>` acts as a `cd ..` command, moving you up one directory and automatically refreshing the file tree.

### 3. Universal Numpad Bridge
* **The Problem:** Linux X-Servers and Tkinter often misinterpret Numpad arrow keys (e.g., `<KP_Up>`) depending on the NumLock state, causing navigation to fail.
* **v8 Improvement:** A new `bridge_numpad` helper function explicitly binds all Numpad navigational keys (`KP_Up`, `KP_Down`, `KP_Home`, etc.) to generate their standard Arrow Key equivalents. This ensures seamless cursor movement in the Code Editor and File Explorer regardless of your keyboard hardware.
* ---
* ## 📥 Setup and Installation

### For Linux (Native) & WSL
Ensure you have the following packages installed based on your distribution.

```bash
sudo dnf update
# Install Python, UI, and Image components
sudo dnf install python3-tkinter python3-pillow-tk
# Install EDA Toolchain
sudo dnf install iverilog gtkwave yosys graphviz

