## Introduction 
**Bash** (short for *Bourne Again Shell*) is a command-line interpreter used in operating systems like Linux and macOS that allows users to interact with the system using text commands. It was created in 1989 by Brian Fox as part of the GNU Project. Bash was designed to replace the older Bourne Shell (sh), adding more powerful features like scripting, command history, and easier automation. The main reason Bash was developed was to provide a free and improved shell for Unix-like systems, helping users and developers efficiently control their systems, automate tasks, and manage files and programs through simple commands instead of graphical interfaces.

## Basic Command 
###  File & Directory

* `pwd` → Show current folder
* `ls` → List files
* `ls -l` → Detailed list
* `cd folder` → Go into folder
* `cd ..` → Go back
* `mkdir name` → Create folder
* `rm file` → Delete file
* `rm -r folder` → Delete folder

###  File Handling

* `touch file.txt` → Create file
* `cat file.txt` → Show content
* `nano file.txt` → Edit file
* `cp a.txt b.txt` → Copy file
* `mv a.txt b.txt` → Rename/move

---

###  Search & Find

* `find . -name file.txt` → Find file
* `grep "text" file.txt` → Search inside file

---

###  System Info

* `whoami` → Current user
* `uname -a` → System info
* `top` → Running processes

---

###  Network

* `ping google.com` → Check internet
* `ifconfig` → Network info

---

###  Package (Debian/Ubuntu)

* `sudo apt update` → Update list
* `sudo apt upgrade` → Upgrade system
* `sudo apt install pkg` → Install package


### Pro Shortcuts

* `clear` → Clean screen
* `history` → Show past commands
* `Ctrl + C` → Stop command
* `Ctrl + L` → Clear screen (shortcut)
* `Tab` → Auto-complete

##  Syntax

```
command [options] [arguments]
```
Example:

```
ls -l /home
```

* `ls` → command
* `-l` → option
* `/home` → argument

## Variables

**Definition:** Variables store data that can be reused later in the script.

```bash
name="Dark"
echo $name
```


## Control Structures

**Definition:** Control structures manage the flow of execution (decision-making and looping).

```bash
if [ condition ]; then
  echo "Yes"
fi
```


## Boolean Operators

**Definition:** Used to combine or compare conditions (true/false logic).

```bash
if [ $a -gt 5 ] && [ $b -lt 10 ]; then
  echo "Both true"
fi
```

* `&&` → AND
* `||` → OR
* `!` → NOT

---

## Numeric Operators

**Definition:** Used to compare numbers.

```bash
if [ $a -eq $b ]; then
  echo "Equal"
fi
```

* `-eq` → equal
* `-ne` → not equal
* `-gt` → greater than
* `-lt` → less than
* `-ge` → greater or equal
* `-le` → less or equal


## String Operators

**Definition:** Used to compare text values.

```bash
if [ "$name" = "Dark" ]; then
  echo "Match"
fi
```

* `=` → equal
* `!=` → not equal
* `-z` → empty string
* `-n` → not empty

## If Statements

**Definition:** Used to execute code based on a condition.

```bash
if [ $age -gt 18 ]; then
  echo "Adult"
else
  echo "Minor"
fi
```

---

## Inline If Statements

**Definition:** Short form of if-else in a single line.

```bash
[ $age -gt 18 ] && echo "Adult" || echo "Minor"
```

---

## While Loops

**Definition:** Repeats code while a condition is true.

```bash
count=1
while [ $count -le 3 ]; do
  echo $count
  ((count++))
done
```

## For Loops

**Definition:** Repeats code for a fixed range or list.

```bash
for i in {1..3}; do
  echo $i
done
```


## Case Statements

**Definition:** Used for multiple condition matching (like switch).

```bash
read choice

case $choice in
  1) echo "Option 1" ;;
  2) echo "Option 2" ;;
  *) echo "Invalid" ;;
esac
```

Here is your **Final Advanced Bash Cheat Sheet (with short definitions)**:

---

## Functions

**Definition:** Functions are reusable blocks of code to perform a specific task.

```bash id="c6z2p1"
greet() {
  echo "Hello, $1"
}

greet "Dark"
```

## File Operations

**Definition:** Used to create, read, copy, move, and delete files.

```bash id="z7u2xv"
touch file.txt
cp file.txt backup.txt
mv file.txt new.txt
rm file.txt
```

## Check Disk Usage

**Definition:** Shows how much disk space is used and available.

```bash id="1vnt8u"
df -h
```

## Monitor CPU Usage

**Definition:** Displays real-time CPU and process usage.

```bash id="b9w3qk"
top
```

---

## Display System Information

**Definition:** Shows details about the system.

```bash id="0k6qph"
uname -a
```

---

## Backup Files

**Definition:** Creates a copy of important files for safety.

```bash id="d3h9cx"
cp file.txt /backup/
```

## Check Network Connectivity

**Definition:** Tests if the system can reach another server.

```bash id="zq0n1s"
ping google.com
```

## Check Available Memory

**Definition:** Displays RAM usage and availability.

```bash id="0s5d9k"
free -h
```

## Monitor Disk Usage of a Specific Directory

**Definition:** Shows space used by a specific folder.

```bash id="b8r2md"
du -sh /home/user
```

## List Running Processes

**Definition:** Displays currently running processes.

```bash id="a8v7wx"
ps aux
```

## Display Current Date and Time

**Definition:** Shows system date and time.

```bash id="3j8hru"
date
```


## Generate Random Password

**Definition:** Creates a random secure password.

```bash id="r4c9pn"
openssl rand -base64 12
```


## Check System Load Average

**Definition:** Shows system workload over time.

```bash id="v2k6ds"
uptime
```

## Monitor Network Traffic

**Definition:** Displays network activity.

```bash id="p9x1zt"
ifconfig
```

## Search for a File

**Definition:** Finds files by name or pattern.

```bash id="k3m7qe"
find / -name file.txt
```

## Display System Users

**Definition:** Lists users currently logged in.

```bash id="z8p2lf"
who
```

## Check System Uptime

**Definition:** Shows how long the system has been running.

```bash id="n1q7sv"
uptime
```

Here is your **Final Bash Cheat Sheet (Text Processing & Compression with short definitions)**:

## Text Processing

**Definition:** Used to read, filter, and manipulate text data.

```bash id="7w2l0m"
cat file.txt
grep "word" file.txt
awk '{print $1}' file.txt
sed 's/old/new/' file.txt
```

## Replace in Files

**Definition:** Used to find and replace text inside files.

```bash id="9p3x2k"
sed -i 's/old/new/g' file.txt
```

## Symbolic Links

**Definition:** A shortcut (link) that points to another file or directory.

```bash id="5r8d1q"
ln -s target.txt link.txt
```

## Compressing Files

**Definition:** Reduces file size to save space.

### zip

**Definition:** Compress files into `.zip` format.

```bash id="1x7v9c"
zip archive.zip file.txt
```

### gzip

**Definition:** Compress a file into `.gz` format.

```bash id="2m4k8n"
gzip file.txt
```

### tar -c

**Definition:** Create an archive (can combine multiple files).

```bash id="3n6j0b"
tar -cvf archive.tar folder/
```

## Decompressing Files

**Definition:** Extract compressed files.

### unzip

**Definition:** Extract `.zip` files.

```bash id="6b9q2z"
unzip archive.zip
```

---

### gunzip

**Definition:** Extract `.gz` files.

```bash id="8t5h3w"
gunzip file.txt.gz
```


### tar -x

**Definition:** Extract `.tar` archives.

```bash id="4y1c7p"
tar -xvf archive.tar
```

Here is your **Final Bash Cheat Sheet (System, Network & Advanced Concepts with short definitions)**:


## Command-Line Arguments

**Definition:** Values passed to a script from the terminal.

```bash id="x2k9a1"
echo "First: $1"
echo "Second: $2"
```

## Common Utilities

**Definition:** Basic commands used for everyday tasks.

```bash id="u7p3v8"
echo "Hello"
clear
history
man ls
```


## HTTP Requests

**Definition:** Used to send requests to web servers.

```bash id="m4q8z2"
curl https://example.com
wget https://example.com/file.zip
```

## Network Troubleshooting

**Definition:** Helps diagnose network issues.

```bash id="k8n2s5"
ping google.com
traceroute google.com
netstat -tuln
```

## DNS

**Definition:** Resolves domain names to IP addresses.

```bash id="z1c7x9"
nslookup google.com
dig google.com
```

## Hardware

**Definition:** Shows system hardware information.

```bash id="p6t4y2"
lscpu
lsblk
free -h
```

## Terminal Multiplexers

**Definition:** Run multiple terminal sessions in one window.

```bash id="q9r5w1"
tmux
screen
```

## Secure Shell Protocol (SSH)

**Definition:** Connect securely to remote systems.

```bash id="a3d7f0"
ssh user@host
```

## Secure Copy

**Definition:** Transfer files securely between systems.

```bash id="s8g2h6"
scp file.txt user@host:/path/
```

---

## Bash Profile

**Definition:** Configuration file that runs when a shell starts.

```bash id="j4k9l2"
nano ~/.bashrc
```

---

## Bash Script

**Definition:** A file containing Bash commands for automation.

```bash id="w5e8r3"
#!/bin/bash
echo "Hello World"
```

## Variables

**Definition:** Store data for reuse in scripts.

```bash id="c2v7b9"
name="Dark"
echo $name
```

## Environment Variables

**Definition:** Global variables available system-wide.

```bash id="n8m1p4"
echo $HOME
export NAME="Dark"
```

## Functions

**Definition:** Reusable blocks of code.

```bash id="t3y6u0"
myfunc() {
  echo "Hello"
}
myfunc
```

## Exit Codes

**Definition:** Status code returned by a command (0 = success).

```bash id="b1n9k7"
echo $?
```

Here is your **Final Bash Cheat Sheet (Control Flow, Debugging & Pro Usage with short definitions)**:


## Conditional Statements

**Definition:** Used to control execution flow based on conditions.

```bash id="v1k9x3"
if [ $a -gt 5 ]; then
  echo "True"
fi
```

## Boolean Operators

**Definition:** Combine multiple conditions (true/false logic).

```bash id="b7n2q6"
if [ $a -gt 5 ] && [ $b -lt 10 ]; then
  echo "Valid"
fi
```

* `&&` → AND
* `||` → OR
* `!` → NOT


## Numeric Operators

**Definition:** Compare numeric values.

```bash id="k3m8z1"
[ $a -eq $b ]
```

* `-eq`, `-ne`, `-gt`, `-lt`, `-ge`, `-le`


## String Operators

**Definition:** Compare string values.

```bash id="p4x6d9"
[ "$name" = "Dark" ]
```

* `=`, `!=`, `-z`, `-n`

## If Statements

**Definition:** Execute code based on a condition.

```bash id="q9w2e5"
if [ $age -gt 18 ]; then
  echo "Adult"
else
  echo "Minor"
fi
```

---

## Inline If Statements

**Definition:** Short one-line conditional execution.

```bash id="r8t1y7"
[ $age -gt 18 ] && echo "Adult" || echo "Minor"
```

## While Loops

**Definition:** Repeat code while condition is true.

```bash id="u5i3o2"
i=1
while [ $i -le 3 ]; do
  echo $i
  ((i++))
done
```

## For Loops

**Definition:** Repeat code over a fixed range or list.

```bash id="l2k8m4"
for i in {1..3}; do
  echo $i
done
```

## Case Statements

**Definition:** Handle multiple conditions (like switch-case).

```bash id="c7v9b1"
case $1 in
  start) echo "Starting" ;;
  stop) echo "Stopping" ;;
  *) echo "Unknown" ;;
esac
```

## Input/Output Redirectors

**Definition:** Control input and output of commands.

```bash id="n6m3z8"
echo "Hello" > file.txt
cat file.txt >> file.txt
command < input.txt
```

* `>` → overwrite
* `>>` → append
* `<` → input

## Command Line Processing Cycle

**Definition:** How Bash reads and executes commands step by step.

```bash id="d4f7g2"
# Read → Parse → Execute → Output
```

## Debugging Script

**Definition:** Find and fix errors in scripts.

```bash id="h9j2k5"
bash -x script.sh
```

---

## Colors and Styles

**Definition:** Add colors to terminal output.

```bash id="s3d8f6"
echo -e "\e[31mRed Text\e[0m"
```

## Tips and Tricks

**Definition:** Small techniques to work faster.

```bash id="w1q4e7"
!!        # run last command
!ls       # run last ls command
```

## Shortcut Keys

**Definition:** Keyboard shortcuts for faster terminal use.

* `Ctrl + C` → stop
* `Ctrl + L` → clear
* `Ctrl + A` → start of line
* `Ctrl + E` → end of line
* `Tab` → auto-complete

## Best Practices

**Definition:** Recommended ways to write clean and safe scripts.

* Use meaningful variable names
* Always quote variables: `"$var"`
* Check errors using exit codes
* Keep scripts simple and readable
* Add comments for clarity
