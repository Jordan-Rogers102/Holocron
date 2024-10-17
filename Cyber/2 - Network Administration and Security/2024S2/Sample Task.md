>[!tip] This is an example of how to complete sections for [Assessment 2 - 2024S2](Cyber/2%20-%20Network%20Administration%20and%20Security/2024S2/Assessment%202%20-%202024S2.md)



# Project Overview


# Code

The goal of the script in this project is to automate the update and configuration of a newly installed Operating System (Raspberry Pi). This particular script configures the Website Server with a MariaDB database backend. 

## System Requirements

This BASH script assumes that the operating system is:
- Raspberry Pi or Linux (Debian/Ubuntu) based
- Clean, newly installed OS.
- Internet connectivity

This script has been written to be installed on Raspberry Pi hardware or a virtual machine ([Raspberry Pi Desktop](https://www.raspberrypi.com/software/raspberry-pi-desktop/) installed in virtualisation software such as VirtualBox).

This script has been tested on:
- Raspberry PI 400 (link)
- Raspberry Pi Desktop (32Bit, Kernel v5.10, Debian v11 (bullseye))

This script assumes the user has familiarity with the console/terminal.

```bash
#!/bin/bash

echo "Host Name: $(hostname)"
echo "OS Version: $(cat /etc/issue)"
echo "Uptime: $(uptime -p)"

sudo apt update

sudo apt install ntpdate -y
echo "Setting Australia/Canberra timezone"
cp /usr/share/zoneinfo/Australia/Canberra /etc/localtime

# Defining colours
# from : https://unix.stackexchange.com/questions/92563/friendly-terminal-color-names-in-shell-scripts

red='\e[1;31m%s\e[0m\n'
green='\e[1;32m%s\e[0m\n'
yellow='\e[1;33m%s\e[0m\n'
blue='\e[1;34m%s\e[0m\n'
magenta='\e[1;35m%s\e[0m\n'
cyan='\e[1;36m%s\e[0m\n'


system=`arch`
if [ $system = "i686" ]; then
    # echo "Rasperry Pi 32-bit detected, on Desktop"
    printf "$magenta" "Raspbian on PC/Mac"
elif [ $system = "aarch64" ]; then

    # echo "Rasperry Pi OS 64 Bit"
    printf "$green"   "Raspbian on Raspberry Pi 64bit"

    echo "Syncing time with NTP server"
    sudo ntpdate 203.62.5.5
else
    # echo "Rasperry Pi OS 32 Bit"
    printf "$blue"   "Raspbian on Raspberry Pi 32bit"

    echo "Syncing time with NTP server"
    sudo ntpdate 203.62.5.5
fi

sudo apt dist-upgrade -y

# Option 1: Install Apache2, MySQL and PHP together
sudo apt install apache2 mysql-server -y

# Option 2: Install Apache2, MySQL and PHP individually
# sudo apt install apache2 -y
# sudo apt install mysql-server -y
# sudo apt install apache3 -y

sudo apt autoremove -y # Remove unnecessary packages
sudo apt clean # Clean up the package cache
```

The specific goals of this script are (in no specific order):
- Check the Architecture of the CPU
- Sets the current time
- Outputs details on the OS
- Updates the OS to the latest version.*
- Cleans up old packages
- Installs the required server packages


## CPU Architecture
```bash
system=`arch`
if [ $system = "i686" ]; then
    # echo "Rasperry Pi 32-bit detected, on Desktop"
    printf "$magenta" "Raspbian on PC/Mac"
elif [ $system = "aarch64" ]; then
    # echo "Rasperry Pi OS 64 Bit"
    printf "$green"   "Raspbian on Raspberry Pi 64bit"
    echo "Syncing time with NTP server"
    sudo ntpdate 203.62.5.5
else
    # echo "Rasperry Pi OS 32 Bit"
    printf "$blue"   "Raspbian on Raspberry Pi 32bit"
    echo "Syncing time with NTP server"
    sudo ntpdate 203.62.5.5
fi
```

This section of the script detects what the underlying CPU architecture of the Operating System is.

Currently, this script identifies the following Architectures:

| Architecture | Operating System                                       |
| ------------ | ------------------------------------------------------ |
| i686         | Virtual Machine on PC/Mac running Raspberry Pi Desktop |
| aarch64      | Raspberry Pi Hardware running 64-bit Raspberry Pi OS   |
| other        | Raspberry Pi Hardware running 32-bit Raspberry Pi OS   |
`aarch64` refers to a 64-bit CPU running ARM architecture. In the case of Raspberry Pis, this part of the code will run if it's a modern Raspberry Pi, and it's been tested on a Raspberry Pi 400 with the latest OS. This should execute on other Raspberry Pis running 64-bit OSs, but hasn't been tested.

The script could be updated to output the architecture with the other [[Cyber/2 - Network Administration and Security/2024S2/Sample Task#OS Details|OS Details]]. This would require refactoring the script so that the architecture is read prior to the OS detail output. This could be done like so, but hasn't been tested:

```bash
echo "Host Name: $(hostname)"
echo "OS Version: $(cat /etc/issue)"
echo "Uptime: $(uptime -p)"
echo $system
```

## Current Time

## OS Details

## Update OS

## Clean up Old Packages

## Server Installation

## Server Configuration






# Data



# Development Process


# Technical Skills


# Development Process


