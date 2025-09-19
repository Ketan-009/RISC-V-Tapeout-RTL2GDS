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

## Yosys Installation Guide

## System Update
It's recommended to update your system before installing new software. Run the following commands:

```bash
sudo apt-get update
sudo apt-get install make  # If make is not installed
```

## Build Dependencies
Yosys requires several dependencies for a successful build. Install the necessary packages using the following command:

```bash
sudo apt install git build-essential clang bison flex libreadline-dev \
libgmp-dev libmpfr-dev libmpc-dev
```

## Clone/Build Instructions
Follow these steps to clone and build Yosys:

1. Clone the Yosys repository:

    ```bash
    git clone https://github.com/YosysHQ/yosys.git
    cd yosys
    ```

2. Build Yosys:

    ```bash
    make
    ```

3. Optionally, install Yosys to your system:

    ```bash
    sudo make install
    ```

Congratulations! You have successfully installed Yosys on your system.

---

*Generated on: 2025-09-19*
*System Owner: Ketan-009*
