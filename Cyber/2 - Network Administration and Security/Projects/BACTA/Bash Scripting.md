>[!info] Written by Google Gemini
# Overview
**What is Bash Scripting?**

Bash scripting is a powerful tool that allows you to automate tasks and streamline processes in the command line environment. It involves creating text files (.sh files) that contain commands and logic to perform specific actions.

**Why Use Bash Scripting on Raspberry Pi?**

- **Automates repetitive tasks:** Run complex commands with a single script.
- **Customises the Raspberry Pi:** Create personalised scripts for your specific needs.
- **Simplifies system management:** Perform administration tasks like backing up, updating, and installing software.
- **Interacts with hardware:** Control GPIO pins, sensors, and other peripherals.

**Getting Started**

1. Open a terminal window (e.g., lxterminal).
2. Create a new script file using the following command:

```bash
touch my_script.sh
```

3. Open the script file in a text editor (e.g., nano):

```bash
nano my_script.sh
```

**Basic Syntax**

- **Comments:** Start with a hash (#) for lines that are not executed.
- **Commands:** Write Linux commands as you would in the terminal.
- **Variables:** Use $variable_name to store and retrieve values.

**Example Scripts**

**Example 1：Display System Information**

```bash
#!/bin/bash

echo "Host Name: $(hostname)"
echo "OS Version: $(cat /etc/issue)"
echo "Uptime: $(uptime -p)"
```

**Example 2：Check if a File Exists**

```bash
#!/bin/bash

FILE="myfile.txt"

if [ -f "$FILE" ]; then
  echo "File $FILE exists."
else
  echo "File $FILE does not exist."
fi
```

**Example 3：Creating and Deleting directory**

```bash
#!/bin/bash

DIR="mydirectory"

mkdir $DIR
echo "Directory $DIR created."
rm -r $DIR
echo "Directory $DIR removed."
```

**Running Scripts**

1. Make the script executable using:

```
chmod +x my_script.sh
```

2. Run the script by typing its name in the terminal:

```
./my_script.sh
```

**Debugging Scripts**

- Use the `-x` option to echo each command before executing it.
- Add `echo "some text"` statements to print debug messages.
- Check the exit status of commands using `$?`.

**Conclusion**

Bash scripting is a versatile tool that can significantly enhance your Raspberry Pi experience. By automating tasks and customising your system, you can save time, improve productivity, and unleash the full potential of your device.

# Task

Write a bash script to automate the installation and configuration of your server.

## Steps

The steps needed for this task are:
1. Create bash script file.
2. Enter the command to indicate it's a Bash script
3. Write the commands to update the Raspberry Pi to the latest version.
4. Write the commands to install the required software
5. Write the commands to configure the server to operate correctly.
6. Test the script

## Details

Start by creating a new text file in your GitHub Classroom repository with any name but with the `.sh` extension.

E.g. `emailServerInstall.sh

Open the file in a text editor and add the first line to indicate it is a bash script:

```bash
#!/bin/bash
```

The next step is to enter an `update` and `dist-upgrade` command to ensure the Raspberry Pi OS is the most up-to-date version.

> [!tip] Research `apt` in order to get the commands needed to complete the update and dist-upgrade processes.

After the script updates the OS to the latest version, then write commands to install and configure the required software for your server.

Finally, run the script on a fresh install of the Raspberry Pi operating system. Note any errors, fix the script, run it again.

# Configuration Script

The script developed in class, current is:

```bash
#!/bin/bash

userResponse = ""

echo "This script will update the OS to the latest version, install NTP and set the timezone to Australia/Canberra"
echo "It will also install Apache2, MySQL and PHP"
echo "Please ensure you have an active internet connection before running this script"

while [[ "$userResponse" != "y" && "$userResponse" != "n" ]]; do
read -p "Are you sure you want to continue? (y/n)" userResponse
userResponse = ${userResponse,,} # tolower
done

if [ "$userResponse" == "n" ]; then
    echo "Exiting script"
    exit 1
elif  ["$userResponse" == "y" ]; then

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

fi
```

