# 🔧 Yosys Installation Guide

<div align="center">

![Yosys Logo](https://yosyshq.net/yosys/images/yosys_logo.png)

**A Framework for RTL Synthesis**

[![GitHub](https://img.shields.io/badge/GitHub-YosysHQ/yosys-blue?logo=github)](https://github.com/YosysHQ/yosys)
[![Documentation](https://img.shields.io/badge/Docs-yosyshq.net-green)](https://yosyshq.net/yosys/)
[![License](https://img.shields.io/badge/License-ISC-yellow)](https://github.com/YosysHQ/yosys/blob/master/COPYING)

</div>

---

## 📋 Table of Contents

- [🎯 Overview](#-overview)
- [⚙️ Prerequisites](#️-prerequisites)
- [🔄 System Update](#-system-update)
- [📦 Build Dependencies](#-build-dependencies)
- [🚀 Clone and Build Yosys](#-clone-and-build-yosys)
- [✅ Verification](#-verification)
- [🔧 Troubleshooting](#-troubleshooting)
- [📚 Additional Resources](#-additional-resources)

---

## 🎯 Overview

**Yosys** is a framework for **RTL synthesis** and verification, essential for digital design workflows. This guide provides step-by-step instructions for installing Yosys on Ubuntu/Debian systems as part of your **RISC-V Tapeout RTL2GDS** journey.

### Key Features:
- 🔄 **RTL Synthesis**: Convert Verilog to gate-level netlists
- 🎯 **Technology Mapping**: Support for various FPGA and ASIC libraries
- 🔍 **Formal Verification**: Built-in verification capabilities
- 🧩 **Extensible**: Plugin architecture for custom flows

---

## ⚙️ Prerequisites

> **📝 Note**: Ensure you meet these requirements before proceeding

### System Requirements:
- 🐧 **OS**: Ubuntu 18.04+ / Debian 10+ (or compatible Linux distribution)
- 💾 **RAM**: Minimum 4GB (8GB+ recommended for large designs)
- 💿 **Storage**: At least 2GB free space
- ⚡ **CPU**: Multi-core processor recommended for faster builds

### Knowledge Prerequisites:
- Basic terminal/command line usage
- Understanding of file permissions (`sudo` usage)
- Familiarity with Git version control

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

**Expected Output:**
```
Yosys 0.xx (git sha1 xxxxxxxx, gcc x.x.x -Os)
```

### Interactive Test

Test the interactive shell:

```bash
# Start Yosys interactive mode
yosys

# In the Yosys shell, try:
help
# List available commands

# Exit the shell
exit
```

### Basic Synthesis Test

Create a simple test file to verify synthesis functionality:

```bash
# Create a simple Verilog file
cat > test.v << 'EOF'
module test(input a, b, output y);
  assign y = a & b;
endmodule
EOF

# Run synthesis
yosys -p "read_verilog test.v; synth; write_verilog test_synth.v"
```

---

## 🔧 Troubleshooting

### Common Issues & Solutions

<details>
<summary>❌ Build fails with missing dependencies</summary>

**Solution**: Re-run the dependency installation command and ensure all packages are installed:
```bash
sudo apt-get update
sudo apt-get install -f  # Fix broken dependencies
```

</details>

<details>
<summary>❌ Permission denied during installation</summary>

**Solution**: Ensure you're using `sudo` for system-wide installation:
```bash
sudo make install
```

</details>

<details>
<summary>❌ Out of memory during build</summary>

**Solution**: 
- Use fewer parallel jobs: `make -j2` instead of `make -j$(nproc)`
- Ensure at least 4GB RAM available
- Close other applications during build

</details>

<details>
<summary>❌ Git submodule issues</summary>

**Solution**: Manually update submodules:
```bash
cd yosys
git submodule update --init --recursive --force
```

</details>

### Performance Tips

- 🚀 **Faster builds**: Use `make -j$(nproc)` to utilize all CPU cores
- 💾 **Save space**: Remove build artifacts after installation with `make clean`
- ⚡ **Optimization**: Consider using `clang` compiler for potentially faster builds

---

## 📚 Additional Resources

### 📖 Documentation & Learning
- [📘 Yosys Manual](https://yosyshq.net/yosys/documentation.html)
- [🎓 Yosys Tutorial](https://github.com/YosysHQ/yosys/tree/master/docs/source/tutorials)
- [📝 Command Reference](https://yosyshq.net/yosys/cmd_index.html)

### 🛠️ Related Tools
- [OpenROAD](https://openroad.readthedocs.io/) - Place and Route
- [Magic](http://opencircuitdesign.com/magic/) - Layout Tool
- [Netgen](http://opencircuitdesign.com/netgen/) - LVS Tool

### 🌐 Community & Support
- [💬 GitHub Discussions](https://github.com/YosysHQ/yosys/discussions)
- [🐛 Issue Tracker](https://github.com/YosysHQ/yosys/issues)
- [📧 Mailing List](https://lists.sourceforge.net/lists/listinfo/yosys-announce)

---

<div align="center">

## 🎉 Congratulations!

**Yosys is now successfully installed on your system!**

You're ready to proceed with your **RISC-V Tapeout RTL2GDS** journey.

---

*Installation completed: 2025-09-19 19:13:36 UTC*  
*Guide created for: Ketan-009/RISC-V-Tapeout-RTL2GDS*

[![Next: OpenROAD Installation](https://img.shields.io/badge/Next-OpenROAD%20Installation-blue?style=for-the-badge)](https://openroad.readthedocs.io/en/latest/user/Build.html)

</div>
