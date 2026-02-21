# Silicon scaffold Workbench (POC v6)

**Silicon scaffold Workbench v6** (internally designated as the "Leader Key" build) focuses heavily on keyboard-driven productivity and workflow speed. This release minimizes reliance on the mouse by introducing Vim-inspired navigation and customizable keybindings.

---

##  What's New in POC v6 (Improvements)

This version introduces several advanced UI control mechanisms compared to POC v5:

### 1. Vim-Style Leader Key Navigation
* **Global Prefix Key:** You no longer need to click between panes to start typing. By pressing the "Leader Key" (the **`** backtick/grave key), the IDE enters a rapid-switch mode.
* **Instant Pane Switching:** After pressing the leader key, pressing a follow-up key instantly moves your keyboard focus to a specific pane:
  * **` + c** : Focuses the Code Editor.
  * **` + x** : Focuses the Interactive Terminal.
  * **` + v** : Focuses the Project Explorer.
  * **` + z** : Focuses the Schematic Viewer.
* **Dynamic UI Tooltips:** The frame titles for each pane now dynamically display their assigned shortcut key (e.g., `Code (\`+c)`), so you never have to guess or memorize the bindings.

### 2. Customizable Keyboard Settings Menu
* **GUI Settings Window:** A new **⚙ Settings** button has been added to the top toolbar.
* **Live Remapping:** Clicking this opens a dedicated "Keyboard Settings" popup where you can view and edit the focus switch keys on the fly. Changes are saved immediately and update the UI tooltips automatically.

### 3. Smart Spacebar Auto-Completion
* **Terminal Upgrade:** In POC v5, tab-completion in the terminal occasionally conflicted with standard Tkinter UI navigation. In POC v6, this has been entirely rewritten to use a **Smart Spacebar**.
* **How it works:** When in `[SHELL]` mode, typing a partial file or folder name and hitting the `<Space>` bar will evaluate the directory. If there is a unique match, it automatically completes the path. If there is no match or multiple matches, it simply types a standard space, making terminal navigation incredibly fluid.

### 4. Crosshair Visual Cues
* To ensure you know when the IDE is listening for a shortcut, the mouse cursor temporarily turns into a "crosshair" the moment you press the leader key. It resets to a standard arrow as soon as the shortcut is completed or after a 1-second timeout.
* ---
* ### For Linux (Native) & WSL
Ensure you have the following packages installed based on your distribution.

```bash
sudo dnf update
# Install Python, UI, and Image components
sudo dnf install python3-tkinter python3-pillow-tk
# Install EDA Toolchain
sudo dnf install iverilog gtkwave yosys graphviz
