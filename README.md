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

1. Install a Linux distribution (e.g., Ubuntu, Fedora) on your system or set up a virtual machine using VirtualBox or VMware.
2. Ensure you have sudo access to install necessary tools and perform analysis.

### Tools

- `volatility` - Memory forensics framework
- `dd` - Utility for copying and converting files
- `ps` - Report a snapshot of current processes
- `netstat` - Network statistics
- `grep` - Search through text
- `strings` - Find printable strings in files
- `awk` - Pattern scanning and processing language

## Exercises

### Exercise 1: Capturing Memory

Objective: Learn how to capture the memory of a Linux system for forensic analysis to ensure volatile data is preserved for examination.

Step1:  **Install `dd` if not already installed:**
```bash
   sudo apt-get install coreutils
```
Expected Output: dd and other core utilities installed on the system.

Step2: Capture the memory using dd:

```bash
sudo dd if=/dev/mem of=/root/memory_dump.mem bs=1M
```
Expected Output: Memory dump saved to /root/memory_dump.mem.

Step3: Verify the memory dump file:

```bash
ls -lh /root/memory_dump.mem
```
Expected Output: File listing showing the size and location of the memory dump.

### Exercise 2: Setting Up Volatility for Memory Analysis
Objective: Install and set up Volatility, a memory forensics framework, to analyze the captured memory dump.

Step1: Install Volatility
```bash
sudo apt-get install volatility
```
Expected Output: Volatility installed on the system.

Step2: Verify Volatility installation

```bash
volatility --help
```
Expected Output: Help menu of Volatility, confirming successful installation.

Step3: Identify the profile of the memory dump

```bash
volatility -f /root/memory_dump.mem imageinfo
```
Expected Output: Suggested profile(s) for the memory dump.

### Exercise 3: Analyzing Running Processes
Objective: Analyze the running processes in the memory dump to identify suspicious or malicious activities.

Step1: List running processes
```bash
volatility -f /root/memory_dump.mem --profile=LinuxUbuntu16_04x64 pslist
```
Expected Output: List of processes running at the time of the memory capture.

Step2: Search for hidden processes:

```bash
volatility -f /root/memory_dump.mem --profile=LinuxUbuntu16_04x64 pstree
```
Expected Output: Tree view of processes, helping to identify parent-child relationships and hidden processes.

Step3: Compare with live process list

```bash
ps aux
```
Expected Output: Current running processes on the live system for comparison.

### Exercise 4: Investigating Network Connections
Objective: Examine network connections in the memory dump to uncover active and potentially malicious network activities.

Step1: List network connections:

```bash
volatility -f /root/memory_dump.mem --profile=LinuxUbuntu16_04x64 netscan
```
Expected Output: List of network connections at the time of the memory capture, including TCP and UDP connections.

Step2: Analyze network statistics

```bash
netstat -anp
```
Expected Output: Current network statistics on the live system for comparison.

Step3: Identify suspicious connections:

```bash
volatility -f /root/memory_dump.mem --profile=LinuxUbuntu16_04x64 connscan
```
Expected Output: Detailed information about network connections, including potential hidden or suspicious connections.

### Exercise 5: Extracting and Analyzing Strings
Objective: Extract and analyze strings from the memory dump to find indicators of compromise and other relevant information.

Step1: Extract strings from memory dump:

```bash
strings /root/memory_dump.mem > /root/memory_strings.txt
```
Expected Output: File containing all printable strings from the memory dump.

Step2: Search for specific keywords:

```bash
grep -i "password" /root/memory_strings.txt
```
Expected Output: Lines containing the keyword "password", indicating potential sensitive information.

Step3: Analyze extracted strings:

```bash
less /root/memory_strings.txt
```
Expected Output: Interactive view of the extracted strings, allowing for detailed analysis.

## Conclusion

By completing these exercises, you will gain a foundational understanding of Linux memory forensics, enabling you to capture and analyze memory to detect and investigate malicious activities on a system.

## About Me

I am a cybersecurity trainer with a passion for teaching and helping others learn essential cybersecurity skills through practical, hands-on projects. Connect with me on social media for more updates and resources:

[![LinkedIn](https://img.icons8.com/fluent/48/000000/linkedin.png)](https://www.linkedin.com/in/rajneeshcyber)
[![YouTube](https://img.icons8.com/fluent/48/000000/youtube-play.png)](https://www.youtube.com/@rajneeshcyber)
[![Twitter](https://img.icons8.com/fluent/48/000000/twitter.png)](https://twitter.com/rajneeshcyber)

Feel free to reach out with any questions or feedback. Happy learning!
