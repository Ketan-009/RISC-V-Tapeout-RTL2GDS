# Week 1: System Setup and Environment Configuration

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
