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
 - Clone the LiME repository: git clone https://github.com/504ensicsLabs/LiME.git
 - Compile LiME: Navigate to the LiME directory and run make.
4. Install Volatility:
 - Clone the Volatility repository: git clone https://github.com/volatilityfoundation/volatility.git
 - Install dependencies: Follow the instructions in the Volatility documentation.

### Tools

- `volatility` - Memory forensics framework
- `avml` - Utility for memory aquisition developed by Microsoft
- `ps` - Report a snapshot of current processes
- `netstat` - Network statistics
- `grep` - Search through text
- `strings` - Find printable strings in files
- `awk` - Pattern scanning and processing language

## Exercises

### Exercise 1: Capturing Memory with LiME
Objective: Learn how to capture the memory of a Linux system using LiME.

Steps:

1. Load LiME Module:
```
sudo insmod lime.ko "path=/memory_dump.lime format=lime"
```
2. Verify Memory Dump:
```
ls -lh /memory_dump.lime
```
Expected Output: A memory dump file named memory_dump.lime should be present in the root directory.

3. Unload LiME Module:
```
sudo rmmod lime
```
Expected Output: LiME module should be successfully removed from the kernel.

### Exercise 2: Capturing Memory using AVML

Step1:**: Download AVML** 

Download the executable from https://github.com/microsoft/avml/releases

Step2: Make it executable

```
chmod +x ./kvml
```

Step3: Create a Memory dump

```
sudo ./kvml rajneesh.mem
```

Step4: Test 

```markdown
strings rajneesh.mem | grep "mozilla"
```

### Exercise 3: Setting Up Volatility for Memory Analysis
Objective: Install and set up Volatility, a memory forensics framework, to analyze the captured memory dump.

#### Step 1: Update and Upgrade Your System
First, ensure your system is up to date.
```bash
sudo apt update
sudo apt upgrade -y
```

#### Step 2: Install Python 3
Volatility 3 requires Python 3.

Install Python 3:

```bash
sudo apt install python3 python3-pip python3-dev -y
```
Verify Python Installation:

```bash
python3 --version
```
#### Step 3: Install Dependencies
Install the required packages for Volatility 3.

Install Required Packages:
```bash
sudo apt install build-essential git -y
sudo pip3 install capstone
sudo pip3 install distorm3
sudo pip3 install yara-python
sudo pip3 install pefile
sudo pip3 install pytz
sudo pip3 install jsonschema
```
#### Step 4: Download Volatility 3
Clone the Repository:

```bash
git clone https://github.com/volatilityfoundation/volatility3.git
```
Navigate to the Volatility 3 Directory:

```bash
cd volatility3
```
#### Step 5: Set Up Volatility 3
Run Volatility 3:
```bash
python3 vol.py
```
This should display Volatility 3’s help message.
#### Step 6: Verify the Installation
To ensure Volatility 3 is working correctly, you can run a basic command:

```bash
python3 vol.py -h
```
This command should display the help message with available commands and options.


### Exercise 4: Analyzing Running Processes
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

### Exercise 5: Investigating Network Connections
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

### Exercise 6: Extracting and Analyzing Strings
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
