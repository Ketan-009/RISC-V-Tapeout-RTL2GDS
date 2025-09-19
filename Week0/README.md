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

# ⚡ Ngspice Installation Guide

## 🎯 Overview

**Ngspice** is a mixed-level/mixed-signal electronic circuit simulator based on Berkeley SPICE 3f5. Essential for analog and mixed-signal verification in your RISC-V design flow!

### 🌟 Key Features:
- 🔬 **SPICE Simulation**: Industry-standard circuit simulation
- ⚡ **Mixed-Signal**: Analog, digital, and mixed-signal support
- 📊 **Advanced Analysis**: AC, DC, transient, noise analysis
- 🔧 **Extensible**: Comprehensive model library
- 🎯 **RISC-V Ready**: Perfect for I/O and analog verification
- 🆓 **Open Source**: Free and actively maintained

## 📦 Installation Steps

### Step 1: Download Ngspice Source

Download the latest stable release (v45.2):

```bash
wget -O ngspice-45.2.tar.gz https://sourceforge.net/projects/ngspice/files/ng-spice-rework/45.2/ngspice-45.2.tar.gz/download
```

> **📝 Note**: The download URL redirects from SourceForge, this is normal behavior.

### Step 2: Extract the Archive

```bash
tar -zxvf ngspice-45.2.tar.gz
```
**Output:**
```
ngspice-45.2/
ngspice-45.2/.gitignore
ngspice-45.2/aclocal.m4
ngspice-45.2/ANALYSES
ngspice-45.2/ar-lib
ngspice-45.2/AUTHORS
ngspice-45.2/autogen.sh
ngspice-45.2/BUGS
ngspice-45.2/ChangeLog
...
```

### Step 3: Navigate and Create Build Directory

```bash
cd ngspice-45.2
mkdir release
cd release
```

> **💡 Why separate build directory?** This keeps source clean and allows multiple build configurations.

### Step 4: Configure the Build

Configure with recommended options for RISC-V development:

```bash
../configure --with-x --with-readline=yes --disable-debug
```

### 🔧 Configuration Options Explained:

| Option | Purpose |
|--------|---------|
| `--with-x` | 🖥️ Enable X11 GUI support for plotting |
| `--with-readline=yes` | 📖 Enable command line editing |
| `--disable-debug` | ⚡ Optimize for performance |

### Step 5: Compile Ngspice

```bash
make
```

**Build Progress Indicators:**
- ⏳ **Compilation time**: 5-15 minutes depending on system
- 🔄 **Progress**: Watch for successful compilation messages
- ✅ **Success**: No fatal errors at the end

### Step 6: Install System-wide

```bash
sudo make install
```

### 🚨 **Real Error Encountered**

**Error Message:**
```bash
ketan@ketan:~/ngspice-45.2/release$ make
CDPATH="${ZSH_VERSION+.}:" && cd .. && /bin/bash '/home/ketan/ngspice-45.2/missing' aclocal-1.16 -I m4
/home/ketan/ngspice-45.2/missing: line 81: aclocal-1.16: command not found
WARNING: 'aclocal-1.16' is missing on your system.
         You should only need it if you modified 'acinclude.m4' or
         'configure.ac' or m4 files included by 'configure.ac'.
         The 'aclocal' program is part of the GNU Automake package:
         <https://www.gnu.org/software/automake>
make: *** [Makefile:460: ../aclocal.m4] Error 127
```
## 📷 Snapshot
<img width="1063" height="255" alt="Screenshot 2025-09-20 020639" src="https://github.com/user-attachments/assets/214d7655-9a3a-4f5e-acf5-5a9d889dd082" />

### 🔧 **Solution That Worked**

**Root Cause:** Missing `automake` package which provides `aclocal-1.16`

**Step-by-Step Fix:**

```bash
# Step 1: Install missing automake package
sudo apt-get update
sudo apt-get install automake

# Also ensure you have the complete autotools suite
sudo apt-get install autoconf libtool

# Step 2: Clean the broken build state
cd ~/ngspice-45.2
rm -rf release
rm -f config.cache config.log config.status
rm -f Makefile

# Step 3: Fresh build setup
mkdir release
cd release

# Step 4: Reconfigure and build
../configure --with-x --with-readline=yes --disable-debug
make

# Step 5: Install if successful
sudo make install
```

## ✅ Verification

### Quick Version Check

Verify installation success:

```bash
ngspice --version
```

**Output:**
```
******
** ngspice-45.2 : Circuit level simulation program
** Compiled with KLU Direct Linear Solver
** The U. C. Berkeley CAD Group
** Copyright 1985-1994, Regents of the University of California.
** Copyright 2001-2025, The ngspice team.
** Please get your ngspice manual from https://ngspice.sourceforge.io/docs.html
** Please file your bug-reports at http://ngspice.sourceforge.net/bugrep.html
** Creation Date: Fri Sep 19 20:42:13 UTC 2025
******
```

## 📷 Snapshot
<img width="1073" height="576" alt="image" src="https://github.com/user-attachments/assets/ef680304-3a8c-4b03-8ba9-44f06599c1a6" />

# 🎩 Magic VLSI Installation Guide

## 🎯 Overview

**Magic VLSI** is a venerable VLSI layout tool, written in the 1980s at Berkeley by John Ousterhout. Now maintained by Tim Edwards, it remains one of the most capable layout tools available for academic and open-source use.

### 🌟 Key Features:
- 🎨 **Interactive Layout**: Real-time design rule checking
- 🔍 **Hierarchical Design**: Support for complex chip layouts
- ⚡ **Fast DRC**: Built-in design rule checking
- 🔬 **Parasitic Extraction**: RC and capacitance extraction
- 🎯 **RISC-V Ready**: Perfect for custom RISC-V layouts
- 🆓 **Open Source**: Free with extensive community support

## 📦 Installation Steps

### Step 1: Install All Dependencies

Install the complete dependency chain:

```bash
sudo apt-get update
sudo apt-get install m4
sudo apt-get install tcsh
sudo apt-get install csh
sudo apt-get install libx11-dev
sudo apt-get install tcl-dev tk-dev
sudo apt-get install libcairo2-dev
sudo apt-get install mesa-common-dev libglu1-mesa-dev
sudo apt-get install libncurses-dev
```

> **💡 Pro Tip**: You can combine these into a single command for efficiency

```bash
sudo apt-get install m4 tcsh csh libx11-dev tcl-dev tk-dev \
    libcairo2-dev mesa-common-dev libglu1-mesa-dev libncurses-dev
```

### Step 2: Clone Magic Repository

Clone from the official repository:

```bash
git clone https://github.com/RTimothyEdwards/magic
```

### Step 3: Navigate to Magic Directory

```bash
cd magic
```

### Step 4: Configure the Build

Run the configure script to detect system capabilities:

```bash
./configure
```

### Step 5: Compile Magic

```bash
make
```

### Step 6: Install System-wide

```bash
sudo make install
```

## ✅ Verification

### Quick Version Check

Verify Magic installed correctly:

```bash
magic -version
```

**Output:**
```
8.3.552
```

## 📷 Snapshot
<img width="1919" height="1023" alt="image" src="https://github.com/user-attachments/assets/96bc939e-a7b9-4b03-ac77-e93f3a4ef75f" />





*Generated on: 2025-09-19*
*System Owner: Ketan*
