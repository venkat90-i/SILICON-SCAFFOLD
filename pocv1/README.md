# POC v1

**POC v1** is a lightweight, Python-based Integrated Development Environment (IDE) designed to streamline Verilog HDL development specifically within **Linux environment**. It provides a graphical interface to bridge the gap between simple text editing and powerful open-source command-line EDA tools.

---

## ✨ Key Features

* **Project File Explorer**: Automatically scans your working directory for `.v` files for quick access.
* **Integrated Code Editor**: A clean, focused workspace for writing and editing Verilog modules.
* **One-Click Simulation**: Automates the compilation process using **Icarus Verilog** and execution via **VVP**.
* **Waveform Viewing**: Quickly launch **GTKWave** to visualize signal transitions from generated `.vcd` files.
* **Synthesis Check**: Integrated **Yosys** support to perform quick logic checks and resource utilization reporting.
* **Real-time Console**: An embedded terminal window to view compilation errors and simulation outputs directly.

---

## 🛠️ Prerequisites

To run this IDE, ensure your Linux environment has the following installed:

1.  **Python 3 & Tkinter**:
    ```bash
    sudo apt update
    sudo apt install python3 python3-tk
    ```
2.  **Verilog Toolchain**:
    * **Icarus Verilog** (for compilation and simulation)
    * **GTKWave** (for viewing waveforms)
    * **Yosys** (for synthesis checks)


---

## 🚀 How to Use

### 1. Launching
Navigate to your project directory in the Linux terminal and run:
```bash
python3 pocv1.py
