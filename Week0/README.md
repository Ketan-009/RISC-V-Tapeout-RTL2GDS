# Week 0: System Setup and Environment Configuration

## 🖥️ System Specifications

This document contains the system setup and configuration details for the RISC-V Tapeout RTL2GDS journey.

## 📋 System Check Report

Below is the comprehensive system check script and its output:

### System Check Script

```bash
echo "=================================="
echo "       SYSTEM CHECK REPORT"
echo "=================================="
echo

echo "1. SYSTEM INFO:"
echo "   OS: $(lsb_release -d | cut -f2)"
echo "   Kernel: $(uname -r)"
echo "   Architecture: $(uname -m)"
echo

echo "2. CPU INFO:"
echo "   Cores: $(nproc)"
echo "   Model: $(lscpu | grep 'Model name' | cut -d':' -f2 | xargs)"
echo

echo "3. MEMORY INFO:"
echo "   Total RAM: $(free -h | awk 'NR==2{print $2}')"
echo "   Available: $(free -h | awk 'NR==2{print $7}')"
echo "   Used: $(free -h | awk 'NR==2{print $3}')"
echo

echo "4. STORAGE INFO:"
echo "   Root partition: $(df -h / | awk 'NR==2{print $2 " total, " $4 " available, " $5 " used"}')"
```

### System Check Output

```
==================================
       SYSTEM CHECK REPORT
==================================

1. SYSTEM INFO:
   OS: Ubuntu 22.04.5 LTS
   Kernel: 6.8.0-83-generic
   Architecture: x86_64

2. CPU INFO:
   Cores: 8
   Model: AMD Ryzen 7 7840HS w/ Radeon 780M Graphics

3. MEMORY INFO:
   Total RAM: 7.8Gi
   Available: 6.5Gi
   Used: 928Mi

4. STORAGE INFO:
   Root partition: 98G total, 81G available, 13% used
```
## Snapshot
<img width="1919" height="926" alt="image" src="https://github.com/user-attachments/assets/a7183b9b-798d-4202-877e-e21c3dd53ad8" />

## 💻 System Summary

| Component | Specification |
|-----------|---------------|
| **Operating System** | Ubuntu 22.04.5 LTS |
| **Kernel Version** | 6.8.0-83-generic |
| **Architecture** | x86_64 |
| **Processor** | AMD Ryzen 7 7840HS w/ Radeon 780M Graphics |
| **CPU Cores** | 8 |
| **Total RAM** | 7.8 GiB |
| **Available RAM** | 6.5 GiB |
| **Storage** | 98GB total, 81GB available |

## ✅ System Readiness

The system appears to be well-configured for RISC-V development and tapeout processes:

- ✅ **Sufficient Processing Power**: 8-core AMD Ryzen 7 processor
- ✅ **Adequate Memory**: 7.8GB RAM with 6.5GB available
- ✅ **Ample Storage**: 81GB available storage space
- ✅ **Modern OS**: Ubuntu 22.04.5 LTS with recent kernel
- ✅ **x86_64 Architecture**: Compatible with most EDA tools


# 🔧 Yosys Installation Guide

---

## 🎯 Overview

**Yosys** is a framework for **RTL synthesis** and verification, essential for digital design workflows. This guide provides step-by-step instructions for installing Yosys on Ubuntu/Debian systems as part of your **RISC-V Tapeout RTL2GDS** journey.

### Key Features:
- 🔄 **RTL Synthesis**: Convert Verilog to gate-level netlists
- 🎯 **Technology Mapping**: Support for various FPGA and ASIC libraries
- 🔍 **Formal Verification**: Built-in verification capabilities
- 🧩 **Extensible**: Plugin architecture for custom flows

---


## 🔄 System Update

Start by updating your system packages to ensure compatibility:

```bash
# Update package lists
sudo apt-get update

# Install make if not already present
sudo apt-get install make
```

> **💡 Tip**: It's always good practice to update your system before installing new software packages.

---

## 📦 Build Dependencies

Install all required dependencies for building Yosys. The dependency list includes `libfl-dev` and optionally `lld` for better performance:

```bash
sudo apt-get install build-essential clang lld bison flex libfl-dev \
    libreadline-dev gawk tcl-dev libffi-dev git \
    graphviz xdot pkg-config python3 libboost-system-dev \
    libboost-python-dev libboost-filesystem-dev zlib1g-dev
```

### 📋 Dependency Breakdown:

| Package | Purpose |
|---------|---------|
| `build-essential` | 🔨 Core build tools (gcc, g++, make) |
| `clang` | 🛠️ Modern C/C++ compiler |
| `lld` | ⚡ LLVM linker for better performance |
| `bison` & `flex` | 📝 Parser and lexer generators |
| `libfl-dev` | 🔗 Flex library development files |
| `libreadline-dev` | 📖 Command line editing capabilities |
| `gawk` | 🔧 GNU AWK text processing |
| `tcl-dev` | 🐍 Tool Command Language support |
| `libffi-dev` | 🔌 Foreign Function Interface |
| `git` | 📂 Version control system |
| `graphviz` & `xdot` | 📊 Graph visualization tools |
| `python3` | 🐍 Python interpreter |
| `libboost-*` | 🚀 Boost C++ libraries |
| `zlib1g-dev` | 📦 Compression library |

---

## 🚀 Clone and Build Yosys

### Step 1: Clone Repository

Clone the Yosys repository with all submodules:

```bash
# Clone with submodules (IMPORTANT!)
git clone --recurse-submodules https://github.com/YosysHQ/yosys.git
```

<details>
<summary>🔄 Alternative Method (if you forgot --recurse-submodules)</summary>

```bash
git clone https://github.com/YosysHQ/yosys.git
cd yosys
git submodule update --init --recursive
```

</details>

### Step 2: Build Configuration

Navigate to the yosys directory and configure the build:

```bash
cd yosys
make config-gcc
```

### Step 3: Compile Yosys

Build the project (this may take 5-15 minutes depending on your system):

```bash
# Standard build
make

# Or for faster builds on multi-core systems:
make -j$(nproc)
```

### Step 4: Install System-wide

Install Yosys to make it available system-wide:

```bash
sudo make install
```

---

## ✅ Verification

### Quick Version Check

Verify the installation was successful:

```bash
yosys --version
```

**Output:**
```
Yosys 0.57+148 (git sha1 259bd6fb3, g++ 11.4.0-1ubuntu1~22.04.2 -fPIC -O3)
```

### Interactive Test

Test the interactive shell:

```bash
# Start Yosys interactive mode
yosys
```
## 📷 Snapshot
<img width="1214" height="600" alt="image" src="https://github.com/user-attachments/assets/fbefe4aa-d666-4638-a776-bdf743bf0bdb" />

# ⚡ Iverilog Installation Guide

## 🎯 Overview

**Icarus Verilog (iverilog)** is a free and open-source Verilog simulation and synthesis tool. It's perfect for:

### 🌟 Key Features:
- 🔄 **IEEE 1364 Compliant**: Full Verilog-1995, Verilog-2001, and partial Verilog-2005 support
- ⚡ **Fast Simulation**: Compiled simulation for better performance
- 🎯 **Cross-Platform**: Works on Linux, macOS, and Windows
- 🆓 **Open Source**: Completely free with GPL license
- 🔧 **Easy Integration**: Works seamlessly with other EDA tools

## 📦 Installation Steps

### Step 1: Update Package Repository

Ensure your package lists are up-to-date:

```bash
sudo apt-get update
```

> **📝 Note**: This step fetches the latest package information from Ubuntu repositories.

### Step 2: Install Iverilog

Install Icarus Verilog from the official Ubuntu repository:

```bash
sudo apt-get install iverilog
```

## 📷 Snapshot
<img width="1612" height="862" alt="image" src="https://github.com/user-attachments/assets/2d58e937-1ff4-44fb-86fc-df61dfad743e" />

## ✅ Verification

### Quick Version Check

Verify the installation was successful:

```bash
iverilog -V
```

**Output:**
```
Icarus Verilog version 11.0 (stable) ()

Copyright 1998-2020 Stephen Williams

  This program is free software; you can redistribute it and/or modify
  it under the terms of the GNU General Public License as published by
  the Free Software Foundation; either version 2 of the License, or
  (at your option) any later version.....
```

## 📷 Snapshot

<img width="1919" height="1021" alt="image" src="https://github.com/user-attachments/assets/fb4df76b-b729-4a45-80bd-d158fc0eb3f5" />

# 🌊 GTKWave Installation Guide

## 🎯 Overview

**GTKWave** is a fully featured waveform viewer for digital simulation data. Essential for debugging and analyzing your RISC-V designs!

### 🌟 Key Features:
- 📊 **VCD File Support**: Industry-standard Value Change Dump format
- 🔍 **Signal Analysis**: Zoom, pan, and measure timing relationships
- 🎨 **Customizable Views**: Color coding and signal grouping
- ⚡ **Fast Performance**: Handles large waveform files efficiently
- 🔧 **Search & Filter**: Find signals quickly in complex designs
- 📈 **Multi-format Support**: VCD, LXT, FST, and more

## 📦 Installation Steps

### Step 1: Update Package Repository

Refresh your package database to get the latest versions:

```bash
sudo apt-get update
```

> **📝 Note**: This ensures you get the most recent version available in the repositories.

### Step 2: Install GTKWave

Install GTKWave and its dependencies:

```bash
sudo apt install gtkwave
```

## ✅ Verification

### Quick Version Check

Verify GTKWave installed correctly:

```bash
gtkwave --version
```

**Output:**
```
GTKWave Analyzer v3.3.104 (w)1999-2020 BSI

This is free software; see the source for copying conditions.  There is NO
warranty; not even for MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.
```

## 📷 Snapshot 
<img width="1919" height="1020" alt="image" src="https://github.com/user-attachments/assets/a933469b-2946-4855-992c-afb71c6819d1" />



*Generated on: 2025-09-19*
*System Owner: Ketan*
