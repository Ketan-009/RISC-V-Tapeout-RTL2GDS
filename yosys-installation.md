# Yosys Installation Guide

## Prerequisites
Before you begin the installation, ensure that you have the following prerequisites installed on your system:
- A Unix-like operating system (Linux, macOS).
- Basic knowledge of terminal commands.

## System Update
It's recommended to update your system before installing new software. Run the following commands:

```bash
sudo apt update
sudo apt upgrade
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
