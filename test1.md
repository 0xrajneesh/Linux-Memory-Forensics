# Linux Memory Forensics

## Introduction

Memory forensics is a critical aspect of cybersecurity that involves analyzing volatile data in a system's memory to detect and understand malicious activities. This lab will guide you through the basics of Linux memory forensics, helping you capture and analyze memory to uncover hidden processes, network connections, and other artifacts.    

`Category`: Digital Forensics and Incident Response   
`Sub-Category`: Linux Forensics   
`Level`: Intermediate   

## Pre-requisites

- Basic understanding of Linux commands and file system structure.
- A Linux system or virtual machine with sudo privileges.
- Familiarity with command-line interface (CLI).

## Lab Setup and Tools

### Lab Setup

1. Install VirtualBox/VMware: Download and install VirtualBox or VMware on your host machine.
2. Create a Linux VM: Install a Linux distribution (e.g., Ubuntu) on your virtual machine.
3. Install LiME:
 - Clone the LiME repository: `git clone https://github.com/504ensicsLabs/LiME.git`
 - Compile LiME: Navigate to the LiME directory and run `make`.
4. Install Volatility:
 - Clone the Volatility repository: `git clone https://github.com/volatilityfoundation/volatility.git`
 - Install dependencies: Follow the instructions in the Volatility documentation.

### Tools

- `volatility` - Memory forensics framework
- `avml` - Utility for memory acquisition developed by Microsoft
- `ps` - Report a snapshot of current processes
- `netstat` - Network statistics
- `grep` - Search through text
- `strings` - Find printable strings in files
- `awk` - Pattern scanning and processing language

## Exercises

<details>
<summary>Exercise 1: Capturing Memory with LiME</summary>

**Objective**: Learn how to capture the memory of a Linux system using LiME.

1. Load LiME Module:
    ```bash
    sudo insmod lime.ko "path=/memory_dump.lime format=lime"
    ```
2. Verify Memory Dump:
    ```bash
    ls -lh /memory_dump.lime
    ```
    **Expected Output**: A memory dump file named `memory_dump.lime` should be present in the root directory.

3. Unload LiME Module:
    ```bash
    sudo rmmod lime
    ```
    **Expected Output**: LiME module should be successfully removed from the kernel.
</details>

<details>
<summary>Exercise 2: Capturing Memory using AVML</summary>

Step 1: Download AVML executable from [AVML GitHub releases](https://github.com/microsoft/avml/releases)

Step 2: Make the AVML executable:
```bash
chmod +x ./avml
