# Bash Cheat Sheet

## Introduction

**Bash** (short for *Bourne Again Shell*) is a command-line interpreter used in operating systems like Linux and macOS that allows users to interact with the system using text commands. It was created in **1989** by **Brian Fox** as part of the GNU Project. Bash was designed to replace the older Bourne Shell (`sh`), adding more powerful features like scripting, command history, and easier automation. The main reason Bash was developed was to provide a free and improved shell for Unix-like systems, helping users and developers efficiently control their systems, automate tasks, and manage files and programs through simple commands instead of graphical interfaces.

## Basic Syntax

**Definition:** Every Bash command follows this structure:

```
command [options] [arguments]
```

**Example:**

```bash
ls -l /home
```

* `ls` → command
* `-l` → option (flag)
* `/home` → argument

---

## File & Directory Commands

**Definition:** Commands to navigate, list, create, and remove files and directories.

```bash
pwd               # Show current folder (print working directory)
ls                # List files in current folder
ls -l             # Detailed list (permissions, size, date)
ls -a             # Show hidden files (starting with .)
ls -lh            # Detailed list with human-readable sizes
ls -la            # Detailed list including hidden files

cd folder         # Go into a folder
cd ..             # Go up one level
cd ~              # Go to home directory
cd -              # Go back to previous directory

mkdir name        # Create a new folder
mkdir -p a/b/c    # Create nested folders (no error if exists)

rmdir folder      # Remove an empty folder
rm file           # Delete a file
rm -r folder      # Delete a folder and its contents (recursive)
rm -f file        # Force delete without confirmation
rm -rf folder     # Force delete folder recursively (use carefully!)
```

---

## File Handling

**Definition:** Commands to create, view, copy, move, and edit files.

```bash
touch file.txt        # Create an empty file (or update timestamp)
cat file.txt          # Show full file content
less file.txt         # View file page by page (q to quit)
head file.txt         # Show first 10 lines
head -n 20 file.txt   # Show first 20 lines
tail file.txt         # Show last 10 lines
tail -f file.txt      # Live follow file (useful for logs)

nano file.txt         # Edit file in nano editor
vim file.txt          # Edit file in vim editor

cp a.txt b.txt        # Copy a file
cp -r dir/ dest/      # Copy a folder recursively
mv a.txt b.txt        # Rename or move a file
```

---

## Search & Find

**Definition:** Commands to search for files and text content.

```bash
find . -name file.txt         # Find file by name in current directory
find / -name file.txt         # Find file anywhere on system
find . -type f                # Find only regular files
find . -type d                # Find only directories
find . -size +1M              # Find files larger than 1 MB
find . -mtime -7              # Files modified in last 7 days
find . -name "*.log" -delete  # Find and delete .log files
find . -exec chmod +x {} \;   # Run command on each found file

grep "text" file.txt          # Search for text inside file
grep -i "text" file.txt       # Case-insensitive search
grep -r "text" dir/           # Recursive search in directory
grep -n "text" file.txt       # Show line numbers with matches
grep -v "text" file.txt       # Show lines NOT matching
grep -c "text" file.txt       # Count matching lines
grep -E "pattern" file.txt    # Extended regex search
```

---

## System Info

**Definition:** Commands to view system and hardware information.

```bash
whoami        # Show current logged-in user
uname -a      # Full system and kernel info
uname -r      # Kernel version only
hostname      # Show system hostname
id            # User ID, group ID, and all groups
uptime        # System uptime and load averages
date          # Current date and time
cal           # Display calendar
lscpu         # CPU architecture and core info
lsblk         # Block devices (disks, partitions)
lspci         # PCI devices (GPU, network card, etc.)
lsusb         # USB devices connected
arch          # Machine hardware name (e.g. x86_64)

top           # Real-time CPU and process monitor (q to quit)
htop          # Interactive process viewer (install separately)
free -h       # RAM usage (human-readable)
df -h         # Disk space on all partitions
du -sh dir/   # Size of a specific folder
```

---

## Network

**Definition:** Commands to configure, test, and troubleshoot network connections.

```bash
ifconfig              # Show network interface info (older systems)
ip addr               # Show IP addresses (modern)
ip route              # Show routing table
hostname -I           # Show local IP address(es)

ping google.com       # Check internet connectivity
ping -c 4 google.com  # Send only 4 pings

netstat -tuln         # Show active listening ports
ss -tuln              # Modern replacement for netstat
```

---

## Package Management

**Definition:** Commands to install, update, and remove software packages.

### Debian / Ubuntu (APT)

```bash
sudo apt update           # Refresh package list
sudo apt upgrade          # Upgrade all installed packages
sudo apt install pkg      # Install a package
sudo apt remove pkg       # Remove a package (keep config)
sudo apt purge pkg        # Remove package + config files
sudo apt autoremove       # Remove unused dependencies
apt search keyword        # Search for a package
apt show pkg              # Show package details
dpkg -l                   # List all installed packages
```

### RHEL / Fedora (DNF / YUM)

```bash
sudo dnf update           # Update all packages
sudo dnf install pkg      # Install a package
sudo dnf remove pkg       # Remove a package
sudo yum install pkg      # Older RHEL/CentOS syntax
```

---

## Variables

**Definition:** Variables store data that can be reused later in a script. No spaces around the `=` sign.

```bash
name="Dark"           # Declare a string variable
age=25                # Declare a number variable
readonly PI=3.14      # Read-only (constant) variable
unset name            # Delete a variable

echo $name            # Access variable value
echo "${name}!"       # Use variable inside string
echo ${#name}         # Get length of string variable
num=$((5 + 3))        # Arithmetic assignment
```

**Example:**

```bash
name="Dark"
echo "Hello, $name!"
# Output: Hello, Dark!
```

---

## Environment Variables

**Definition:** Global variables available across all processes. Set with `export`.

```bash
echo $HOME      # Home directory path
echo $USER      # Current username
echo $PATH      # Directories searched for commands
echo $SHELL     # Current shell path
echo $PWD       # Current working directory
echo $OLDPWD    # Previous working directory
echo $?         # Exit code of last command (0 = success)

export NAME="Dark"          # Export variable to child processes
printenv                    # Print all environment variables
```

---

## Special Variables

**Definition:** Built-in variables with special meanings inside scripts.

| Variable | Meaning |
|----------|---------|
| `$0` | Script name |
| `$1`, `$2` | First, second argument |
| `$#` | Total number of arguments |
| `$@` | All arguments (separate words) |
| `$*` | All arguments (single string) |
| `$$` | PID of current shell |
| `$!` | PID of last background process |
| `$?` | Exit status of last command |

**Example:**

```bash
#!/bin/bash
# Run: bash script.sh Alice 25
echo "Script name: $0"
echo "First arg:   $1"
echo "Total args:  $#"
echo "All args:    $@"
```

---

## String Operations

**Definition:** Manipulate and extract parts of string variables using parameter expansion.

```bash
str="Hello World"

echo ${str^^}           # Uppercase → HELLO WORLD
echo ${str,,}           # Lowercase → hello world
echo ${str:6:5}         # Substring (start 6, length 5) → World
echo ${str/World/Bash}  # Replace first match → Hello Bash
echo ${str//o/0}        # Replace all matches → Hell0 W0rld
echo ${str#Hello }      # Remove prefix → World
echo ${str##* }         # Remove longest prefix → World (last word)
echo ${str% *}          # Remove suffix → Hello (first word)

name=""
echo ${name:-"Guest"}   # Use default if empty → Guest
echo ${name:="Guest"}   # Set and use default if unset
```

---

## Arithmetic

**Definition:** Perform math operations in Bash scripts.

```bash
a=10
b=3

echo $((a + b))     # Addition → 13
echo $((a - b))     # Subtraction → 7
echo $((a * b))     # Multiplication → 30
echo $((a / b))     # Integer division → 3
echo $((a % b))     # Remainder (modulo) → 1
echo $((a ** 2))    # Power → 100

((a++))             # Increment a by 1
((a--))             # Decrement a by 1
((a += 5))          # Add 5 to a

# Floating point math (bc needed)
echo "scale=2; 10 / 3" | bc    # Output: 3.33
```

---

## Boolean Operators

**Definition:** Used to combine or compare conditions (true/false logic).

```bash
if [ $a -gt 5 ] && [ $b -lt 10 ]; then
  echo "Both true"
fi

if [ $a -gt 20 ] || [ $b -lt 10 ]; then
  echo "At least one true"
fi

if ! [ $a -eq 0 ]; then
  echo "a is not zero"
fi
```

| Operator | Meaning |
|----------|---------|
| `&&` | AND — both must be true |
| `\|\|` | OR — at least one must be true |
| `!` | NOT — negate the condition |

---

## Numeric Operators

**Definition:** Used to compare numeric values in conditions.

```bash
if [ $a -eq $b ]; then
  echo "Equal"
fi
```

| Operator | Meaning |
|----------|---------|
| `-eq` | Equal |
| `-ne` | Not equal |
| `-gt` | Greater than |
| `-lt` | Less than |
| `-ge` | Greater than or equal |
| `-le` | Less than or equal |

---

## String Operators

**Definition:** Used to compare text/string values.

```bash
if [ "$name" = "Dark" ]; then
  echo "Match"
fi
```

| Operator | Meaning |
|----------|---------|
| `=` | Equal |
| `!=` | Not equal |
| `-z` | String is empty |
| `-n` | String is not empty |

---

## File Test Operators

**Definition:** Check if a file or directory exists and its type/permissions.

```bash
if [ -f "file.txt" ]; then echo "Is a regular file"; fi
if [ -d "folder" ];   then echo "Is a directory"; fi
if [ -e "path" ];     then echo "Exists (file or dir)"; fi
if [ -r "file" ];     then echo "Readable"; fi
if [ -w "file" ];     then echo "Writable"; fi
if [ -x "file" ];     then echo "Executable"; fi
if [ -s "file" ];     then echo "Not empty (size > 0)"; fi
if [ -L "file" ];     then echo "Is a symbolic link"; fi
```

---

## If Statements

**Definition:** Execute different code blocks based on conditions.

```bash
if [ $age -gt 65 ]; then
  echo "Senior"
elif [ $age -gt 17 ]; then
  echo "Adult"
elif [ $age -gt 12 ]; then
  echo "Teen"
else
  echo "Child"
fi
```

---

## Inline If Statements

**Definition:** Short one-line conditional execution.

```bash
[ $age -gt 18 ] && echo "Adult" || echo "Minor"

# Safer grouped form
[ $age -gt 18 ] && { echo "Adult"; } || { echo "Minor"; }
```

---

## Case Statements

**Definition:** Match a variable against multiple patterns — like a switch/case in other languages.

```bash
read -p "Enter choice: " choice

case $choice in
  1)   echo "Option 1 selected" ;;
  2)   echo "Option 2 selected" ;;
  3)   echo "Option 3 selected" ;;
  q|Q) echo "Quitting..." ;;
  *)   echo "Invalid choice" ;;
esac
```

---

## While Loops

**Definition:** Repeats a code block while the condition remains true.

```bash
count=1
while [ $count -le 5 ]; do
  echo "Count: $count"
  ((count++))
done
```

**Read file line by line:**

```bash
while IFS= read -r line; do
  echo "Line: $line"
done < file.txt
```

---

## For Loops

**Definition:** Repeats code for a fixed range, list, or array.

```bash
# Numeric range
for i in {1..5}; do
  echo "Number: $i"
done

# Range with step (0, 2, 4, 6, 8, 10)
for i in {0..10..2}; do
  echo $i
done

# C-style for loop
for ((i=0; i<5; i++)); do
  echo "i = $i"
done

# Loop over files
for file in *.sh; do
  echo "Script: $file"
done

# Loop over a list
for fruit in apple banana cherry; do
  echo "Fruit: $fruit"
done
```

---

## Until Loops

**Definition:** Opposite of `while` — runs until the condition becomes true.

```bash
count=1
until [ $count -gt 5 ]; do
  echo "Count: $count"
  ((count++))
done
```

---

## Select Loop

**Definition:** Creates an interactive numbered menu for user selection.

```bash
select color in "Red" "Green" "Blue" "Quit"; do
  case $color in
    "Quit") break ;;
    *)      echo "You picked: $color" ;;
  esac
done
```

---

## Arrays

**Definition:** An ordered list of values stored in a single variable.

```bash
fruits=("apple" "banana" "cherry")   # Declare array

echo "${fruits[0]}"       # Access first element → apple
echo "${fruits[@]}"       # All elements
echo "${#fruits[@]}"      # Number of elements → 3
echo "${!fruits[@]}"      # All indices → 0 1 2

fruits+=("mango")         # Append element
fruits[1]="blueberry"     # Update element at index 1
unset fruits[2]           # Delete element at index 2

# Loop over array
for fruit in "${fruits[@]}"; do
  echo "→ $fruit"
done
```

---

## Associative Arrays

**Definition:** Key-value pairs (like dictionaries). Requires Bash 4+.

```bash
declare -A user                # Declare associative array

user["name"]="Dark"
user["age"]="25"
user["city"]="Mumbai"

echo "${user["name"]}"         # Dark
echo "${!user[@]}"             # All keys
echo "${user[@]}"              # All values

# Loop over key-value pairs
for key in "${!user[@]}"; do
  echo "$key → ${user[$key]}"
done
```

---

## Functions

**Definition:** Functions are reusable blocks of code that perform a specific task. They can accept arguments and return values.

```bash
# Define a function
greet() {
  local name="$1"        # local variable (only inside this function)
  echo "Hello, $name!"
}

greet "Dark"             # Call function → Hello, Dark!
greet "World"            # Hello, World!


# Function with return value
add() {
  echo $(( $1 + $2 ))
}

result=$(add 5 3)
echo "Sum: $result"      # Sum: 8
```

---

## Exit Codes

**Definition:** Every command returns an exit code. `0` means success, any non-zero value means an error.

```bash
echo $?         # Print exit code of last command

exit 0          # Exit script successfully
exit 1          # Exit script with error

# Enable strict mode (recommended for scripts)
set -e          # Exit on any error
set -u          # Treat unset variables as error
set -o pipefail # Catch errors inside pipes
```

---

## Input / Output Redirection

**Definition:** Control where command input comes from and where output goes.

```bash
echo "Hello" > file.txt     # Write stdout to file (overwrite)
echo "World" >> file.txt    # Append stdout to file
command < input.txt         # Use file as stdin
command 2> error.log        # Redirect stderr to file
command 2>&1                # Redirect stderr to stdout
command &> file.txt         # Redirect both stdout and stderr
command > /dev/null         # Discard stdout (silent)
command 2>/dev/null         # Discard stderr (silent)
command &>/dev/null         # Discard all output
```

| Symbol | Meaning |
|--------|---------|
| `>` | Overwrite stdout |
| `>>` | Append stdout |
| `<` | Read from file as input |
| `2>` | Redirect stderr |
| `2>&1` | Merge stderr into stdout |
| `&>` | Redirect all output |

---

## Pipes

**Definition:** Pass the output of one command as input to the next using `|`.

```bash
ls -l | grep ".sh"               # Filter ls output
cat file.txt | sort | uniq       # Sort and deduplicate
ps aux | grep nginx              # Find nginx process

# tee: write to file AND show output
echo "Log" | tee -a logfile.txt

# xargs: build command from stdin
find . -name "*.tmp" | xargs rm
```

---

## Text Processing

**Definition:** Commands to read, filter, search, and manipulate text data.

```bash
cat file.txt                       # Print full file content

# grep — search
grep "word" file.txt               # Find matching lines
grep -i "word" file.txt            # Case-insensitive
grep -n "word" file.txt            # With line numbers

# sed — stream editor (find & replace)
sed 's/old/new/' file.txt          # Replace first match per line
sed 's/old/new/g' file.txt         # Replace all matches
sed -i 's/old/new/g' file.txt      # In-place edit (modifies file)
sed '/^$/d' file.txt               # Delete blank lines

# awk — column/field processing
awk '{print $1}' file.txt          # Print first column
awk -F: '{print $1}' /etc/passwd   # Use : as delimiter
awk '{sum+=$1} END{print sum}' f   # Sum a column

# cut — extract columns
cut -d: -f1 file.txt               # Cut field 1 with : delimiter
cut -c1-10 file.txt                # Cut first 10 characters

# sort & uniq
sort file.txt                      # Sort alphabetically
sort -n file.txt                   # Sort numerically
sort -r file.txt                   # Sort in reverse
uniq file.txt                      # Remove duplicate adjacent lines
uniq -c file.txt                   # Count each duplicate

# tr — translate characters
echo "hello" | tr 'a-z' 'A-Z'     # Uppercase conversion
echo "a b c" | tr -d ' '          # Delete spaces

# wc — word/line count
wc -l file.txt     # Count lines
wc -w file.txt     # Count words
wc -c file.txt     # Count bytes
```

---

## File Operations

**Definition:** Used to create, read, copy, move, delete, and manage files.

```bash
touch file.txt          # Create empty file
cat file.txt            # Read file content
cp file.txt backup.txt  # Copy file
mv file.txt newname.txt # Rename / move file
rm file.txt             # Delete file

# Generate random password
openssl rand -base64 12

# Display current date and time
date

# Show who is logged in
who

# Show login history
last
```

---

## Compression & Archiving

**Definition:** Commands to compress, archive, and extract files.

### Create Archives

```bash
tar -cvf archive.tar folder/        # Create tar archive
tar -czvf archive.tar.gz folder/    # Create gzip-compressed tar
tar -cjvf archive.tar.bz2 folder/  # Create bzip2-compressed tar
gzip file.txt                       # Compress to .gz (replaces original)
zip archive.zip file.txt            # Create zip file
zip -r archive.zip folder/          # Zip entire folder
```

### Extract Archives

```bash
tar -xvf archive.tar                # Extract tar
tar -xzvf archive.tar.gz            # Extract gzip tar
tar -xjvf archive.tar.bz2           # Extract bzip2 tar
gunzip file.txt.gz                  # Decompress .gz file
unzip archive.zip                   # Extract zip file
unzip archive.zip -d /target/dir/   # Extract to specific folder
```

### View Without Extracting

```bash
tar -tvf archive.tar.gz             # List contents of archive
unzip -l archive.zip                # List contents of zip
```

---

## Symbolic Links

**Definition:** A symbolic link is a shortcut that points to another file or directory.

```bash
ln -s target.txt link.txt      # Create symbolic (soft) link
ln target.txt hardlink.txt     # Create hard link

ls -l                          # View links (shown with ->)
readlink link.txt              # Show where link points
unlink link.txt                # Remove symbolic link
```

---

## Permissions & Ownership

**Definition:** Control who can read, write, and execute files and directories.

### chmod — Change Permissions

```bash
chmod 755 file.sh       # rwxr-xr-x (owner all, others read+exec)
chmod 644 file.txt      # rw-r--r-- (owner rw, others read)
chmod 600 secret.key    # rw------- (owner only)
chmod +x file.sh        # Add execute for all
chmod -x file.sh        # Remove execute
chmod u+w file          # Add write for owner (u=user, g=group, o=others)
chmod go-w file         # Remove write for group and others
chmod -R 755 dir/       # Apply recursively to directory
```

| Permission | Value |
|------------|-------|
| `r` (read) | 4 |
| `w` (write) | 2 |
| `x` (execute) | 1 |

### chown — Change Ownership

```bash
chown user file           # Change file owner
chown user:group file     # Change owner and group
chown -R user dir/        # Change ownership recursively
```

---

## Process Management

**Definition:** View, monitor, and control running processes.

```bash
ps aux              # List all running processes
ps -ef              # Full-format process list
pgrep nginx         # Find PID by process name
kill PID            # Send SIGTERM (graceful stop)
kill -9 PID         # Force kill (SIGKILL)
killall name        # Kill all processes by name
pkill name          # Kill by name pattern

bg                  # Resume stopped job in background
fg                  # Bring background job to foreground
jobs                # List background jobs in current shell
cmd &               # Run command in background
nohup cmd &         # Run immune to hangup in background
```

---

## Disk & Memory

**Definition:** Monitor storage and memory usage.

```bash
df -h               # Disk space on all mounted filesystems
df -h /home         # Disk space for specific partition
du -sh dir/         # Total size of a directory
du -sh *            # Size of each item in current directory

free -h             # RAM usage (human-readable)
vmstat              # Virtual memory stats
uptime              # System uptime and load averages
```

---

## SSH & Remote

**Definition:** Securely connect to and transfer files to remote systems.

```bash
ssh user@host               # SSH login
ssh -p 2222 user@host       # SSH on custom port
ssh-keygen                  # Generate SSH key pair
ssh-copy-id user@host       # Copy public key to server

scp file.txt user@host:/path/    # Upload file (secure copy)
scp user@host:file.txt .         # Download file from server
rsync -avz src/ dest/            # Sync files locally
rsync -avz src/ user@host:dest/  # Sync to remote server
```

---

## HTTP Requests

**Definition:** Send HTTP requests to web servers from the terminal.

```bash
curl https://example.com              # Fetch URL content
curl -O url                           # Download with original filename
curl -o file.zip url                  # Download with custom name
curl -I url                           # Show response headers only
curl -X POST url                      # POST request
curl -d '{"key":"val"}' -H "Content-Type: application/json" url  # POST with JSON
wget url                              # Download file
wget -r url                           # Recursive website download
```

---

## DNS & Network Troubleshooting

**Definition:** Diagnose network issues and resolve domain names.

```bash
ping google.com             # Test connectivity
traceroute google.com       # Trace route (hops) to host
mtr google.com              # Live ping + traceroute combined
netstat -tuln               # Show active listening ports
ss -tuln                    # Modern replacement for netstat

nslookup google.com         # DNS lookup
dig google.com              # Detailed DNS query
dig +short google.com       # Short DNS answer
host google.com             # Simple DNS lookup
whois domain.com            # WHOIS registration info
```

---

## Hardware Info

**Definition:** View detailed system hardware information.

```bash
lscpu          # CPU architecture, cores, threads
lsblk          # Block devices (disks and partitions)
lspci          # PCI devices (GPU, network card, etc.)
lsusb          # USB devices
free -h        # RAM availability
uname -a       # Full system and kernel info
```

---

## Terminal Multiplexers

**Definition:** Run multiple terminal sessions inside a single window. Useful for remote sessions.

### tmux

```bash
tmux                    # Start new session
tmux new -s name        # Start named session
tmux ls                 # List sessions
tmux attach -t name     # Attach to session
tmux kill-session -t n  # Kill a session
```

**Inside tmux (Ctrl+b is the prefix key):**

| Shortcut | Action |
|----------|--------|
| `Ctrl+b d` | Detach from session |
| `Ctrl+b c` | Create new window |
| `Ctrl+b %` | Split pane vertically |
| `Ctrl+b "` | Split pane horizontally |
| `Ctrl+b arrow` | Move between panes |
| `Ctrl+b x` | Close current pane |

### screen

```bash
screen               # Start screen session
screen -S name       # Start named session
screen -r            # Reattach to session
Ctrl+a d             # Detach from session
```

---

## Bash Script

**Definition:** A Bash script is a plain text file containing Bash commands, used for automation.

```bash
#!/usr/bin/env bash          # Shebang — use portable form
# OR
#!/bin/bash                  # Fixed path form

echo "Hello, World!"
```

**Make it executable and run:**

```bash
chmod +x script.sh    # Give execute permission
./script.sh           # Run the script
bash script.sh        # Run with bash directly
bash -n script.sh     # Check syntax (don't run)
bash -x script.sh     # Debug (trace each command)
```

**Read user input:**

```bash
read -p "Enter your name: " name
echo "Hello, $name!"

read -s -p "Password: " pass   # Silent input (for passwords)
```

---

## Bash Profile & Aliases

**Definition:** Configuration files that run when your shell starts. Customize your environment here.

| File | When it runs |
|------|-------------|
| `~/.bashrc` | Every interactive shell |
| `~/.bash_profile` | Login shells |
| `~/.bash_aliases` | Alias file (source from `.bashrc`) |

```bash
nano ~/.bashrc        # Edit config file
source ~/.bashrc      # Reload without restarting shell
. ~/.bashrc           # Shorthand for source
```

**Add custom aliases:**

```bash
# Add to ~/.bashrc
alias ll='ls -lah'
alias ..='cd ..'
alias gs='git status'
alias myip='curl -s ifconfig.me'
alias update='sudo apt update && sudo apt upgrade -y'

# Custom function
mkcd() { mkdir -p "$1" && cd "$1"; }

# Custom PATH
export PATH="$HOME/.local/bin:$PATH"
```

**Alias commands:**

```bash
alias              # List all current aliases
alias name='cmd'   # Create an alias
unalias name       # Remove an alias
\cmd               # Run command bypassing alias
```

---

## Debugging Scripts

**Definition:** Techniques to find and fix errors in Bash scripts.

```bash
bash -n script.sh     # Syntax check (no execution)
bash -x script.sh     # Trace mode — print each command before running

# Inside script:
set -x              # Enable trace mode from this point
set +x              # Disable trace mode

set -e              # Exit on any error
set -u              # Error on unset variables
set -o pipefail     # Catch errors inside pipes

# Trap errors
trap 'echo "Error on line $LINENO"' ERR
trap 'echo "Script exiting"; cleanup' EXIT
```

**Command Line Processing Cycle:**

```
Read → Parse → Expand → Redirect → Execute → Output
```

---

## Colors and Styles

**Definition:** Add colors and formatting to terminal output using ANSI escape codes.

```bash
echo -e "\e[31mRed Text\e[0m"
echo -e "\e[32mGreen Text\e[0m"
echo -e "\e[33mYellow Text\e[0m"
echo -e "\e[34mBlue Text\e[0m"
echo -e "\e[1mBold Text\e[0m"
echo -e "\e[4mUnderline Text\e[0m"
```

**Using variables for clean scripts:**

```bash
RED='\e[31m'
GREEN='\e[32m'
YELLOW='\e[33m'
BOLD='\e[1m'
RESET='\e[0m'

echo -e "${BOLD}${GREEN}Success:${RESET} Build complete"
echo -e "${RED}Error:${RESET} File not found"
echo -e "${YELLOW}Warning:${RESET} Disk almost full"
```

| Code | Effect |
|------|--------|
| `\e[31m` | Red |
| `\e[32m` | Green |
| `\e[33m` | Yellow |
| `\e[34m` | Blue |
| `\e[1m` | Bold |
| `\e[4m` | Underline |
| `\e[0m` | Reset all |

---

## Shortcut Keys

**Definition:** Keyboard shortcuts for faster terminal use.

| Shortcut | Action |
|----------|--------|
| `Ctrl + C` | Stop / kill current command |
| `Ctrl + Z` | Suspend current process |
| `Ctrl + D` | Exit shell / send EOF |
| `Ctrl + L` | Clear screen |
| `Ctrl + A` | Move cursor to start of line |
| `Ctrl + E` | Move cursor to end of line |
| `Ctrl + U` | Delete from cursor to start |
| `Ctrl + K` | Delete from cursor to end |
| `Ctrl + W` | Delete previous word |
| `Ctrl + R` | Reverse search command history |
| `Tab` | Auto-complete command or filename |
| `Tab Tab` | Show all completions |
| `Alt + .` | Insert last argument of previous command |

---

## Tips and Tricks

**Definition:** Small but powerful techniques to work faster and smarter in Bash.

```bash
!!          # Repeat last command
!ls         # Run last command that started with 'ls'
!$          # Last argument of previous command
!N          # Run command number N from history
Ctrl+R      # Search command history interactively

history             # Show past commands
history | grep git  # Search history for specific command

# Run previous command with sudo
sudo !!

# Swap two files
mv file.txt file.txt.bak && mv file2.txt file.txt && mv file.txt.bak file2.txt

# Quick backup
cp config.json config.json.bak

# Show HISTCONTROL to avoid duplicate history entries
export HISTCONTROL=ignoredups:erasedups
export HISTSIZE=10000
```

---

## Best Practices

**Definition:** Recommended guidelines for writing clean, safe, and readable Bash scripts.

```bash
#!/usr/bin/env bash
set -euo pipefail       # Always use strict mode
IFS=$'\n\t'             # Safe IFS for word splitting

# 1. Always quote variables
cp "$src" "$dest"       # Good
cp $src $dest           # Bad — breaks with spaces in names

# 2. Use [[ ]] instead of [ ] for safer tests
if [[ "$name" == "Dark" ]]; then
  echo "Hello"
fi

# 3. Use $() not backticks
result=$(date)          # Good
result=`date`           # Bad — harder to nest and read

# 4. Use local in functions
myfunc() {
  local temp="$1"       # Stays inside function
  echo "$temp"
}

# 5. Check if a command exists before using it
if ! command -v jq &>/dev/null; then
  echo "Error: jq is required" >&2
  exit 1
fi

# 6. Add comments for clarity
# This loop processes all .log files
for file in *.log; do
  process "$file"
done
```

**Summary of rules:**

* Use `#!/usr/bin/env bash` as shebang
* Always use `set -euo pipefail` at top of scripts
* Always quote variables: `"$var"`
* Use `[[` instead of `[` for conditionals
* Use `$(cmd)` instead of backticks
* Use `local` inside functions
* Use meaningful variable names
* Add comments for every non-obvious block
* Check exit codes and handle errors
* Test scripts with `bash -n` before running
