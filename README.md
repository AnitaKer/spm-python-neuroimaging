# 🧠 SPM for Python: Neuroimaging without MATLAB

![Python](https://img.shields.io/badge/Python-3.10%2B-blue)
![SPM](https://img.shields.io/badge/SPM-25-orange)
![License](https://img.shields.io/badge/License-GPLv2-green)

A step-by-step guide to running **Statistical Parametric Mapping (SPM)** completely inside **Jupyter Lab** using Python. This workflow allows you to analyze fMRI/EEG data **without a paid MATLAB license**, utilizing the new SPM25 Python wrapper and the free MATLAB Runtime.

---

## 📸 Overview
This repository demonstrates how to set up the environment, handle the MATLAB Runtime engine, and run the "Mother of All Experiments" (MoAE) dataset tutorial directly from a Jupyter Notebook.

![Snapshot: SPM GUI running inside Jupyter](assets/spm_gui_jupyter.png)
*(Place a screenshot here of your Jupyter Notebook open with the SPM GUI floating on top)*

---

## 🛠 Prerequisites

Before starting, ensure you have:
1.  **Windows, Mac, or Linux** (This guide focuses on Windows 10/11).
2.  **Anaconda** or Miniconda installed.
3.  **Administrator Access** to your computer (Required for installing the Runtime engine).

---

## 🚀 Installation Guide

### Step 1: Create a "Clean Room" Environment
**Critical:** Do not install this in your `base` environment. Conflicting DLL files from other libraries will crash the MATLAB engine. Create a fresh, lightweight environment.

```bash
# Open Anaconda Prompt
conda create -n spm_env python=3.10
conda activate spm_env
```

### Step 2: Install the Wrapper
Install the official SPM Python wrapper and Jupyter Lab.

```bash
pip install spm-python jupyterlab scipy
```
*Note: We install `scipy` to prevent memory warnings during analysis.*

### Step 3: Install the MATLAB Runtime Engine
This is the "engine" that runs the compiled SPM code. 
**⚠️ IMPORTANT:** You must run this command as an **Administrator**.

1.  Close your current terminal.
2.  Right-click "Anaconda Prompt" $\rightarrow$ **Run as Administrator**.
3.  Activate your environment: `conda activate spm_env`
4.  Run the install command:

```bash
spm install
```

*   Follow the prompts (type `yes` to accept license).
*   It will download ~2GB of files.
*   **Success Message:** `Runtime successfully installed at: C:\Program Files\MATLAB\MATLAB Runtime...`

---

## 💻 Usage

### 1. Launching Jupyter
Open a standard terminal (User mode is fine now), activate the environment, and launch Jupyter.

```bash
conda activate spm_env
python -m jupyter lab
```

### 2. Starting SPM
Create a new Python 3 Notebook and run the following code to launch the GUI:

```python
import spm

# 1. Initialize Defaults (Required)
spm.spm('defaults', 'fmri')

# 2. Launch the Interface
spm.spm()
```

![Snapshot: The SPM Startup Menu](assets/spm_menu.png)
*(Place a screenshot of the small 'fMRI/EEG/PET' startup menu here)*

### 3. Running Batch Jobs (Programmatic)
To run preprocessing steps (Realignment, Smoothing) using the Batch Editor:

```python
# Initialize the Jobman
spm.spm_jobman('initcfg')

# Open the Batch Editor window
spm.spm_jobman('interactive')
```

---

## 🐛 Troubleshooting "Hall of Fame"

These are common errors I encountered and how to resolve them.

### 🔴 Error: `[WinError 740] The requested operation requires elevation`
*   **Cause:** You tried to run `spm install` without Admin rights.
*   **Fix:** Close the terminal. Right-click Anaconda Prompt and select **Run as Administrator**.

### 🔴 Error: `SystemError ... mwwebwindowmanager_init_plugin.dll failed`
*   **Cause:** You are using the `(base)` environment. Anaconda's system files are fighting with MATLAB's system files.
*   **Fix:** Create a new, clean environment (`conda create -n spm_env`) as described in Step 1.

### 🔴 Error: `AttributeError: module 'spm' has no attribute 'run'`
*   **Cause:** Using outdated syntax.
*   **Fix:** Use `spm.spm()` instead of `spm.run()`.

### 🔴 Warning: `sparse matrices will be implemented as dense matrices`
*   **Cause:** Missing the Scipy library.
*   **Fix:** Run `!pip install scipy` inside a cell and restart the kernel.

---

## 📂 Dataset: Mother of All Experiments (MoAE)
To follow the standard tutorials, download the **Face Repetition dataset**:
1.  Download: [face_rep.zip](https://www.fil.ion.ucl.ac.uk/spm/data/face_rep/)
2.  Unzip to a local folder (e.g., `Documents/spm_data/`).
3.  Load via the SPM GUI $\rightarrow$ **Display**.

![Snapshot: Brain Scan Loaded](assets/brain_scan_loaded.png)
*(Place a screenshot of the 3-view brain display here)*

---

## 🔗 References
*   [Official SPM Website](https://www.fil.ion.ucl.ac.uk/spm/)
*   [SPM GitHub Repository](https://github.com/spm/spm)
*   [SPM25 Announcement Paper (Tierney et al., 2025)](https://arxiv.org/abs/2501.12081v1)

---
