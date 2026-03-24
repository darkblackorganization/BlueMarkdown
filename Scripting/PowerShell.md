
## Introduction

**PowerShell** is a cross-platform task automation shell and scripting language built on the **.NET framework**. It was created by **Jeffrey Snover** at Microsoft and first released in **2006**. Unlike traditional command-line shells that work with plain text, PowerShell works with **objects** — making it far more powerful for automation, system administration, and DevOps tasks. PowerShell is available on **Windows, Linux, and macOS** (PowerShell 7+). It uses **cmdlets** (pronounced "command-lets") as its core commands, following a consistent `Verb-Noun` naming pattern like `Get-Process`, `Set-Item`, `Remove-File`.


## Basic Syntax

**Definition:** PowerShell commands follow a consistent `Verb-Noun` pattern called **cmdlets**, and are case-insensitive.

```powershell
Verb-Noun -Parameter Value

# Examples
Get-Process                      # Get all running processes
Get-Process -Name "chrome"       # Get chrome process
Stop-Process -Name "notepad"     # Stop notepad
Get-ChildItem -Path C:\Users     # List files in a path
```

**Common approved verbs:**

| Verb | Purpose |
|------|---------|
| `Get` | Retrieve data |
| `Set` | Change/update data |
| `New` | Create something |
| `Remove` | Delete something |
| `Start` | Start a process/service |
| `Stop` | Stop a process/service |
| `Invoke` | Run/execute something |
| `Test` | Check/validate something |
| `Out` | Send output somewhere |
| `Write` | Write output to host |

---

## Getting Help

**Definition:** PowerShell has a built-in help system — always use it to explore cmdlets and parameters.

```powershell
Get-Help Get-Process              # Basic help for a cmdlet
Get-Help Get-Process -Full        # Detailed help with all parameters
Get-Help Get-Process -Examples    # Show usage examples only
Get-Help Get-Process -Online      # Open docs in browser
Get-Help *network*                # Search all help topics with "network"

Update-Help                       # Download latest help files (run as admin)

Get-Command                       # List all available commands
Get-Command -Verb Get             # List all Get-* commands
Get-Command -Noun Process         # List all *-Process commands
Get-Command *service*             # Search commands by keyword

Get-Member                        # Show properties/methods of an object
Get-Process | Get-Member          # Show what properties Process objects have

# Quick parameter lookup
(Get-Command Get-ChildItem).Parameters.Keys
```

---

## Navigation & File System

**Definition:** Commands to navigate directories and manage the file system. PowerShell uses the same `cd`, `ls`, `pwd` aliases for familiarity.

```powershell
Get-Location              # Show current directory (like pwd)
pwd                       # Alias for Get-Location

Set-Location C:\Users     # Change directory (like cd)
cd C:\Users               # Alias for Set-Location
cd ..                     # Go up one level
cd ~                      # Go to home directory
cd -                      # Go to previous directory

Get-ChildItem             # List files and folders (like ls / dir)
ls                        # Alias
dir                       # Alias
Get-ChildItem -Force      # Include hidden files
Get-ChildItem *.txt       # List only .txt files
Get-ChildItem -Recurse    # List recursively (all subfolders)
Get-ChildItem -Directory  # List only directories
Get-ChildItem -File       # List only files

New-Item -ItemType Directory -Name "MyFolder"   # Create folder
mkdir MyFolder                                  # Shorthand
New-Item -ItemType File -Name "notes.txt"       # Create empty file
```

---

## File Handling

**Definition:** Commands to create, copy, move, rename, delete, and read files.

```powershell
# Create
New-Item -Path "C:\file.txt" -ItemType File       # Create file
New-Item -Path "C:\folder" -ItemType Directory    # Create folder

# Read
Get-Content file.txt              # Read full file (like cat)
Get-Content file.txt -Head 10     # First 10 lines
Get-Content file.txt -Tail 10     # Last 10 lines
Get-Content file.txt -Wait        # Live follow (like tail -f)

# Write
Set-Content file.txt "Hello"      # Write (overwrite)
Add-Content file.txt "New line"   # Append to file
Out-File file.txt                 # Redirect output to file

# Copy, Move, Rename
Copy-Item file.txt backup.txt     # Copy file
Copy-Item dir/ dest/ -Recurse     # Copy folder recursively
Move-Item file.txt C:\dest\       # Move file
Rename-Item old.txt new.txt       # Rename file

# Delete
Remove-Item file.txt              # Delete file
Remove-Item folder -Recurse       # Delete folder and contents
Remove-Item *.log                 # Delete all .log files

# Test existence
Test-Path "C:\file.txt"           # Returns True / False
Test-Path "C:\folder" -PathType Container  # Check if directory
```

---

## Variables

**Definition:** Variables in PowerShell start with `$` and are loosely typed by default — PowerShell infers the type automatically.

```powershell
$name = "Dark"               # String variable
$age = 25                    # Integer variable
$pi = 3.14159                # Float variable
$isAdmin = $true             # Boolean variable
$nothing = $null             # Null value

# Access variables
Write-Output $name           # Print variable value
"Hello, $name!"              # String interpolation

# Constants (cannot be changed)
Set-Variable -Name PI -Value 3.14 -Option Constant

# Remove variable
Remove-Variable name         # Delete a variable
$name = $null                # Set to null

# Multiple assignment
$a, $b, $c = 1, 2, 3        # Assign multiple values at once
```

---

## Data Types

**Definition:** PowerShell is strongly typed under the hood — you can explicitly declare types or let PowerShell infer them.

```powershell
[string]$name = "Dark"       # String
[int]$age = 25               # Integer (32-bit)
[long]$big = 9999999999      # Long integer (64-bit)
[double]$pi = 3.14159        # Double-precision float
[bool]$flag = $true          # Boolean ($true / $false)
[datetime]$now = Get-Date    # Date and time
[array]$arr = 1, 2, 3        # Array
[hashtable]$ht = @{}         # Hash table

# Check type of a variable
$name.GetType()              # Returns type info
$name.GetType().Name         # Returns "String"

# Type conversion
[int]"42"                    # String to int → 42
[string]42                   # Int to string → "42"
[double]"3.14"               # String to double → 3.14
```

---

## String Operations

**Definition:** PowerShell strings support interpolation, concatenation, and many built-in methods.

```powershell
$str = "Hello, World!"

# Basic operations
$str.Length                  # String length → 13
$str.ToUpper()               # HELLO, WORLD!
$str.ToLower()               # hello, world!
$str.Trim()                  # Remove leading/trailing whitespace
$str.TrimStart()             # Remove leading whitespace
$str.TrimEnd()               # Remove trailing whitespace

# Search and replace
$str.Contains("World")       # True
$str.StartsWith("Hello")     # True
$str.EndsWith("!")           # True
$str.Replace("World", "PS")  # Hello, PS!
$str.IndexOf("World")        # 7 (position of first match)

# Substring
$str.Substring(7)            # World! (from index 7)
$str.Substring(7, 5)         # World (from index 7, length 5)

# Split and join
$str.Split(",")              # Split into array by comma
"a", "b", "c" -join "-"     # Join array → a-b-c
-join ("a", "b", "c")       # abc

# String interpolation (double quotes only)
$user = "Dark"
"Hello, $user!"              # Hello, Dark!
"Today: $(Get-Date)"         # Embed expression with $()

# Here-string (multiline)
$text = @"
Line one
Line two
Line three
"@
```

---

## Arithmetic Operators

**Definition:** Standard math operators for numeric calculations.

```powershell
$a = 10
$b = 3

$a + $b     # Addition → 13
$a - $b     # Subtraction → 7
$a * $b     # Multiplication → 30
$a / $b     # Division → 3.333...
$a % $b     # Modulo (remainder) → 1
[Math]::Pow($a, 2)    # Power → 100
[Math]::Sqrt(16)      # Square root → 4
[Math]::Round(3.7)    # Round → 4
[Math]::Abs(-5)       # Absolute value → 5

# Assignment operators
$a += 5     # Add 5 to $a
$a -= 3     # Subtract 3
$a *= 2     # Multiply by 2
$a /= 4     # Divide by 4
$a++        # Increment by 1
$a--        # Decrement by 1
```

---

## Comparison Operators

**Definition:** Used to compare values — returns `$true` or `$false`.

```powershell
5 -eq 5        # Equal → True
5 -ne 3        # Not equal → True
5 -gt 3        # Greater than → True
5 -lt 10       # Less than → True
5 -ge 5        # Greater than or equal → True
5 -le 5        # Less than or equal → True

# String comparison (case-insensitive by default)
"abc" -eq "ABC"    # True (case-insensitive)
"abc" -ceq "ABC"   # False (case-sensitive, c prefix)

# String pattern matching
"Hello" -like "He*"       # True (wildcard)
"Hello" -notlike "He*"    # False
"Hello" -match "^He"      # True (regex match)
"Hello" -notmatch "^He"   # False

# Collection membership
3 -in 1, 2, 3, 4          # True
5 -notin 1, 2, 3           # True
1, 2, 3 -contains 2        # True
```

| Operator | Meaning |
|----------|---------|
| `-eq` | Equal |
| `-ne` | Not equal |
| `-gt` | Greater than |
| `-lt` | Less than |
| `-ge` | Greater or equal |
| `-le` | Less or equal |
| `-like` | Wildcard match |
| `-match` | Regex match |
| `-in` | Value in collection |
| `-contains` | Collection contains value |

---

## Logical Operators

**Definition:** Combine multiple conditions together.

```powershell
$a = 8
$b = 3

($a -gt 5) -and ($b -lt 10)   # AND — both must be true → True
($a -gt 20) -or ($b -lt 10)   # OR — at least one true → True
-not ($a -eq 0)                # NOT — negate → True
!($a -eq 0)                    # Shorthand for -not
```

| Operator | Meaning |
|----------|---------|
| `-and` | Both conditions true |
| `-or` | At least one true |
| `-not` or `!` | Negate condition |
| `-xor` | Exactly one true (exclusive or) |

---

## If Statements

**Definition:** Execute different code blocks based on conditions.

```powershell
$age = 20

if ($age -gt 65) {
    Write-Output "Senior"
} elseif ($age -gt 17) {
    Write-Output "Adult"
} elseif ($age -gt 12) {
    Write-Output "Teen"
} else {
    Write-Output "Child"
}

# Ternary-style (PowerShell 7+)
$result = ($age -ge 18) ? "Adult" : "Minor"
Write-Output $result
```

---

## Switch Statements

**Definition:** Match a value against multiple patterns — cleaner than many if/elseif blocks.

```powershell
$day = "Monday"

switch ($day) {
    "Monday"    { Write-Output "Start of work week" }
    "Friday"    { Write-Output "End of work week" }
    "Saturday"  { Write-Output "Weekend!" }
    "Sunday"    { Write-Output "Weekend!" }
    default     { Write-Output "Midweek" }
}

# Switch with -Wildcard
switch -Wildcard ($day) {
    "Mon*"  { Write-Output "Starts with Mon" }
    "Fri*"  { Write-Output "Starts with Fri" }
}

# Switch with -Regex
switch -Regex ("hello123") {
    "^\d+"   { "Starts with number" }
    "[a-z]+" { "Contains lowercase letters" }
}
```

---

## While Loop

**Definition:** Repeats a block of code while the condition is true.

```powershell
$count = 1
while ($count -le 5) {
    Write-Output "Count: $count"
    $count++
}

# Read lines from file
$lines = Get-Content "file.txt"
$i = 0
while ($i -lt $lines.Count) {
    Write-Output $lines[$i]
    $i++
}
```

---

## For Loop

**Definition:** Repeats code a fixed number of times using a counter.

```powershell
# Basic for loop
for ($i = 0; $i -lt 5; $i++) {
    Write-Output "i = $i"
}

# Countdown
for ($i = 10; $i -ge 0; $i--) {
    Write-Output $i
}
```

---

## ForEach Loop

**Definition:** Iterate over each item in a collection (array, list, file lines, etc.).

```powershell
$fruits = "apple", "banana", "cherry"

# foreach loop
foreach ($fruit in $fruits) {
    Write-Output "Fruit: $fruit"
}

# ForEach-Object with pipeline (%)
$fruits | ForEach-Object { Write-Output "→ $_" }

# ForEach-Object shorthand (%)
1..5 | % { Write-Output "Number: $_" }

# ForEach over files
Get-ChildItem *.txt | ForEach-Object {
    Write-Output "File: $($_.Name)"
}
```

---

## Do-While & Do-Until

**Definition:** Loops that run at least once before checking the condition.

```powershell
# Do-While — runs while condition is true
$count = 1
do {
    Write-Output "Count: $count"
    $count++
} while ($count -le 5)


# Do-Until — runs until condition becomes true
$count = 1
do {
    Write-Output "Count: $count"
    $count++
} until ($count -gt 5)
```

---

## Arrays

**Definition:** An ordered collection of values stored in a single variable.

```powershell
# Declare array
$fruits = "apple", "banana", "cherry"
$nums = @(1, 2, 3, 4, 5)       # Explicit array syntax
$range = 1..10                  # Range array (1 to 10)

# Access elements
$fruits[0]                      # First element → apple
$fruits[-1]                     # Last element → cherry
$fruits[1..2]                   # Slice → banana, cherry

# Array info
$fruits.Count                   # Number of elements → 3
$fruits.Length                  # Same as Count

# Modify
$fruits += "mango"              # Add element
$fruits[1] = "blueberry"        # Update element

# Loop over array
foreach ($item in $fruits) {
    Write-Output $item
}

# Array methods
$nums | Sort-Object             # Sort
$nums | Sort-Object -Descending # Sort descending
$nums | Where-Object { $_ -gt 3 }  # Filter → 4, 5
$nums | Measure-Object -Sum     # Sum of all values
```

---

## Hash Tables

**Definition:** Key-value pair collections — like dictionaries in Python or objects in JavaScript.

```powershell
# Declare hash table
$user = @{
    Name  = "Dark"
    Age   = 25
    City  = "Mumbai"
}

# Access values
$user["Name"]                   # Dark
$user.Name                      # Dark (dot notation)

# Modify
$user["Email"] = "dark@example.com"   # Add key
$user.Age = 26                        # Update value
$user.Remove("City")                  # Remove key

# Check existence
$user.ContainsKey("Name")       # True
$user.ContainsValue("Dark")     # True

# Loop over keys
foreach ($key in $user.Keys) {
    Write-Output "$key → $($user[$key])"
}

# Ordered hash table (preserves insertion order)
$ordered = [ordered]@{
    First  = 1
    Second = 2
    Third  = 3
}
```

---

## Functions

**Definition:** Reusable named blocks of code. Can accept parameters and return values.

```powershell
# Basic function
function Greet {
    Write-Output "Hello, World!"
}

Greet    # Call function

# Function with parameters
function Greet-User {
    param ($Name)
    Write-Output "Hello, $Name!"
}

Greet-User "Dark"    # Hello, Dark!

# Function with typed parameters and defaults
function Add-Numbers {
    param (
        [int]$A,
        [int]$B = 0    # Default value
    )
    return $A + $B
}

$result = Add-Numbers -A 5 -B 3
Write-Output "Sum: $result"    # Sum: 8

# Function returning multiple values
function Get-MinMax {
    param ([int[]]$Numbers)
    $min = ($Numbers | Measure-Object -Minimum).Minimum
    $max = ($Numbers | Measure-Object -Maximum).Maximum
    return $min, $max
}

$min, $max = Get-MinMax -Numbers 3, 1, 7, 2, 9
Write-Output "Min: $min, Max: $max"
```

---

## Parameters & Arguments

**Definition:** Advanced parameter declarations for robust, reusable scripts and functions.

```powershell
function Deploy-App {
    param (
        [Parameter(Mandatory=$true)]
        [string]$AppName,               # Required parameter

        [Parameter(Mandatory=$false)]
        [string]$Environment = "dev",   # Optional with default

        [ValidateSet("dev","staging","prod")]
        [string]$Stage = "dev",         # Only allows specific values

        [ValidateRange(1, 65535)]
        [int]$Port = 8080,              # Must be in range

        [switch]$Verbose                # Switch (flag) parameter
    )

    Write-Output "Deploying $AppName to $Environment on port $Port"

    if ($Verbose) {
        Write-Output "Verbose mode enabled"
    }
}

# Call with named parameters
Deploy-App -AppName "MyApp" -Environment "prod" -Port 443 -Verbose

# Call with positional parameters
Deploy-App "MyApp" "prod"
```

---

## Error Handling

**Definition:** Handle and recover from errors gracefully using try/catch/finally blocks.

```powershell
# Try-Catch-Finally
try {
    $result = 1 / 0                 # This will throw an error
    Write-Output "Result: $result"
}
catch {
    Write-Output "Error caught: $($_.Exception.Message)"
}
finally {
    Write-Output "This always runs (cleanup)"
}

# Catch specific error types
try {
    Get-Item "C:\nonexistent.txt" -ErrorAction Stop
}
catch [System.IO.FileNotFoundException] {
    Write-Output "File not found!"
}
catch {
    Write-Output "Some other error: $_"
}

# ErrorAction parameter
Get-Item "missing.txt" -ErrorAction SilentlyContinue  # Suppress error
Get-Item "missing.txt" -ErrorAction Stop               # Treat as terminating
Get-Item "missing.txt" -ErrorAction Continue           # Default behavior

# $Error variable — stores all recent errors
$Error[0]                   # Last error
$Error.Clear()              # Clear error history
```

---

## Pipeline

**Definition:** Pass output of one cmdlet as input to the next using `|`. The `$_` variable represents the current pipeline object.

```powershell
# Basic pipeline
Get-Process | Sort-Object CPU -Descending

# $_  represents current object in pipeline
Get-Process | Where-Object { $_.CPU -gt 10 }
Get-ChildItem | ForEach-Object { $_.Name.ToUpper() }

# Common pipeline pattern
Get-Service |
    Where-Object { $_.Status -eq "Running" } |
    Select-Object Name, Status |
    Sort-Object Name |
    Out-GridView

# Pipeline with Format
Get-Process | Format-Table Name, CPU, WorkingSet -AutoSize
Get-Process | Format-List *         # All properties in list format
Get-Service | Format-Wide Name -Column 4
```

---

## Filtering & Sorting

**Definition:** Commands to filter, sort, select, and group objects in the pipeline.

```powershell
# Where-Object — filter by condition
Get-Process | Where-Object { $_.CPU -gt 5 }
Get-Service | Where-Object Status -eq "Running"     # Simplified syntax

# Select-Object — choose specific properties
Get-Process | Select-Object Name, CPU, Id
Get-Process | Select-Object -First 10              # First 10
Get-Process | Select-Object -Last 5               # Last 5
Get-Process | Select-Object -Unique Name          # Unique values

# Sort-Object — sort by property
Get-Process | Sort-Object CPU                     # Ascending
Get-Process | Sort-Object CPU -Descending         # Descending
Get-Process | Sort-Object Name, CPU               # Sort by multiple props

# Group-Object — group by property
Get-Service | Group-Object Status                 # Group by status

# Measure-Object — calculate stats
Get-Process | Measure-Object CPU -Sum -Average -Maximum -Minimum
Get-Content file.txt | Measure-Object -Line -Word -Character
```

---

## String Formatting & Output

**Definition:** Commands and techniques for displaying formatted output.

```powershell
# Write-Output — sends objects to pipeline
Write-Output "Hello"
Write-Output $variable

# Write-Host — directly to console (not pipeline)
Write-Host "Hello" -ForegroundColor Green
Write-Host "Error" -ForegroundColor Red -BackgroundColor Black

# Write-Verbose, Write-Warning, Write-Error
Write-Verbose "Debug message" -Verbose    # Only shows with -Verbose
Write-Warning "This is a warning"
Write-Error "This is an error"

# Format strings
"Name: {0}, Age: {1}" -f "Dark", 25       # → Name: Dark, Age: 25
"{0:N2}" -f 3.14159                       # → 3.14 (2 decimal places)
"{0:C}" -f 1234.5                         # → currency format
"{0:D}" -f (Get-Date)                     # Date format

# Out- cmdlets
Get-Process | Out-File "processes.txt"    # Save to file
Get-Process | Out-GridView               # Interactive grid (Windows)
Get-Process | Out-String                 # Convert to string
Get-Process | Out-Null                   # Discard output
```

---

## File I/O

**Definition:** Read from and write to files using PowerShell cmdlets.

```powershell
# Read
Get-Content "file.txt"                    # Read all lines as array
Get-Content "file.txt" -Raw              # Read as single string

# Write
Set-Content "file.txt" "Hello"           # Overwrite file
Add-Content "file.txt" "New line"        # Append to file
"Output" | Out-File "file.txt"           # Redirect to file
"Append" | Out-File "file.txt" -Append   # Append mode

# Read CSV
$data = Import-Csv "data.csv"
$data | ForEach-Object { Write-Output $_.Name }

# Write CSV
$objects | Export-Csv "output.csv" -NoTypeInformation

# Read JSON
$json = Get-Content "data.json" -Raw | ConvertFrom-Json
$json.Name

# Write JSON
$object | ConvertTo-Json | Set-Content "output.json"
$object | ConvertTo-Json -Depth 10        # Deep nested JSON

# Read XML
[xml]$xml = Get-Content "data.xml"
$xml.root.item
```

---

## Regular Expressions

**Definition:** Pattern matching using regular expressions — used with `-match`, `-replace`, `Select-String`.

```powershell
# -match operator
"hello123" -match "\d+"           # True — contains digits
$matches[0]                        # "123" — matched text

# -replace operator
"Hello World" -replace "World", "PS"       # Hello PS
"abc123def" -replace "\d+", "NUM"          # abcNUMdef

# Select-String (like grep)
Select-String "error" *.log               # Search files for "error"
Select-String "error" *.log -CaseSensitive
Get-Content file.txt | Select-String "\d{3}-\d{4}"  # Find phone patterns

# Common regex patterns
"test@email.com" -match "^[\w.]+@[\w.]+\.\w{2,}$"  # Email validation
"192.168.1.1" -match "^\d{1,3}(\.\d{1,3}){3}$"     # IP address

# [regex] class methods
[regex]::Match("abc123", "\d+").Value      # "123"
[regex]::Matches("a1b2c3", "\d").Count     # 3
[regex]::Replace("hello", "[aeiou]", "*")  # h*ll*
```

---

## Working with Objects

**Definition:** PowerShell works with .NET objects — you can access properties, call methods, and create custom objects.

```powershell
# Access object properties
$proc = Get-Process -Name "notepad"
$proc.Name          # Property
$proc.Id
$proc.Kill()        # Method call

# Create custom objects
$person = [PSCustomObject]@{
    Name  = "Dark"
    Age   = 25
    Email = "dark@example.com"
}

$person.Name        # Dark

# Add properties to existing object
$person | Add-Member -MemberType NoteProperty -Name "City" -Value "Mumbai"

# Select and expand properties
$procs = Get-Process | Select-Object Name, Id, CPU
$names = Get-Process | Select-Object -ExpandProperty Name   # Array of names

# Convert object to different formats
Get-Process | ConvertTo-Json                  # To JSON string
Get-Process | ConvertTo-Csv                   # To CSV string
$hash | ConvertTo-Json                        # Hash table to JSON
```

---

## Process Management

**Definition:** Start, stop, and monitor running processes.

```powershell
Get-Process                           # List all processes
Get-Process -Name "chrome"            # Get specific process
Get-Process | Sort-Object CPU -Desc   # Sort by CPU usage
Get-Process | Where-Object { $_.WorkingSet -gt 100MB }  # High memory

Start-Process "notepad.exe"           # Start a process
Start-Process "notepad.exe" -Wait     # Start and wait for it to exit
Start-Process "cmd" -Verb RunAs       # Start as administrator

Stop-Process -Name "notepad"          # Stop by name
Stop-Process -Id 1234                 # Stop by PID
Stop-Process -Name "chrome" -Force    # Force kill

# Wait for process
Wait-Process -Name "setup" -Timeout 60   # Wait max 60 seconds

# Check if process is running
$running = Get-Process -Name "notepad" -ErrorAction SilentlyContinue
if ($running) { Write-Output "Notepad is running" }
```

---

## System Information

**Definition:** Retrieve hardware, OS, and system configuration details.

```powershell
# OS and computer info
Get-ComputerInfo                          # Full system info
$env:COMPUTERNAME                         # Computer name
$env:OS                                   # OS name
[System.Environment]::OSVersion          # Detailed OS version

# Hardware
Get-WmiObject Win32_ComputerSystem        # RAM, manufacturer, model
Get-WmiObject Win32_Processor            # CPU details
Get-WmiObject Win32_LogicalDisk          # Disk information

# Modern alternative (CIM — preferred over WMI)
Get-CimInstance Win32_ComputerSystem
Get-CimInstance Win32_Processor
Get-CimInstance Win32_LogicalDisk | Select-Object DeviceID, Size, FreeSpace

# Services
Get-Service                               # List all services
Get-Service -Name "wuauserv"             # Specific service
Start-Service -Name "Spooler"            # Start service
Stop-Service -Name "Spooler"             # Stop service
Restart-Service -Name "Spooler"          # Restart service
Set-Service -Name "Spooler" -StartupType Automatic   # Set startup type

# Event logs
Get-EventLog -LogName System -Newest 20  # Last 20 system events
Get-EventLog -LogName Application -EntryType Error   # Only errors
Get-WinEvent -LogName System -MaxEvents 10           # Modern alternative
```

---

## Network Commands

**Definition:** Test, configure, and troubleshoot network connections.

```powershell
# Basic connectivity
Test-Connection google.com              # Like ping
Test-Connection google.com -Count 4    # Send 4 pings
Test-NetConnection google.com          # Extended connectivity test
Test-NetConnection google.com -Port 443  # Test specific port

# Network configuration
Get-NetIPAddress                        # All IP addresses
Get-NetAdapter                          # Network adapters
Get-NetRoute                            # Routing table
Get-DnsClientServerAddress             # DNS servers

# DNS lookup
Resolve-DnsName google.com             # DNS lookup
Resolve-DnsName google.com -Type MX   # MX records

# HTTP requests
Invoke-WebRequest "https://example.com"                      # Like curl/wget
Invoke-WebRequest "https://example.com" -OutFile "page.html" # Download
Invoke-RestMethod "https://api.github.com/users/github"      # REST API call (returns object)

$headers = @{ Authorization = "Bearer TOKEN" }
Invoke-RestMethod "https://api.example.com/data" -Headers $headers

# Download file
Invoke-WebRequest "https://example.com/file.zip" -OutFile "file.zip"
```

---

## User & Permission Management

**Definition:** Manage local users, groups, and file/folder permissions on Windows.

```powershell
# Local users (Windows)
Get-LocalUser                            # List local users
New-LocalUser "username" -Password (ConvertTo-SecureString "Pass123!" -AsPlainText -Force)
Set-LocalUser "username" -Description "My user"
Remove-LocalUser "username"
Enable-LocalUser "username"
Disable-LocalUser "username"

# Local groups
Get-LocalGroup                           # List all groups
Add-LocalGroupMember -Group "Administrators" -Member "username"
Remove-LocalGroupMember -Group "Administrators" -Member "username"

# File permissions (ACL)
Get-Acl "C:\folder"                      # Get permissions
$acl = Get-Acl "C:\folder"
$acl | Format-List                       # Detailed view

# Set permissions
$rule = New-Object System.Security.AccessControl.FileSystemAccessRule(
    "username", "FullControl", "Allow"
)
$acl.SetAccessRule($rule)
Set-Acl "C:\folder" $acl
```

---

## Registry (Windows)

**Definition:** Read and write Windows Registry keys using the `HKLM:` and `HKCU:` drives.

```powershell
# Navigate registry like file system
Set-Location HKLM:\SOFTWARE\Microsoft
Get-ChildItem HKLM:\SOFTWARE             # List registry keys
Get-ItemProperty HKLM:\SOFTWARE\key     # Get registry values

# Read
Get-ItemPropertyValue "HKLM:\SOFTWARE\Microsoft\Windows NT\CurrentVersion" -Name ProductName

# Write
New-Item "HKCU:\SOFTWARE\MyApp"          # Create new key
New-ItemProperty "HKCU:\SOFTWARE\MyApp" -Name "Version" -Value "1.0" -PropertyType String
Set-ItemProperty "HKCU:\SOFTWARE\MyApp" -Name "Version" -Value "2.0"

# Delete
Remove-ItemProperty "HKCU:\SOFTWARE\MyApp" -Name "Version"
Remove-Item "HKCU:\SOFTWARE\MyApp" -Recurse
```

---

## Modules

**Definition:** Modules are packages of cmdlets, functions, and tools. Import them to extend PowerShell's functionality.

```powershell
# Find modules
Get-Module                               # List imported modules
Get-Module -ListAvailable               # All available modules
Find-Module "Az"                         # Find in PowerShell Gallery

# Install and import
Install-Module "Az" -Scope CurrentUser  # Install from Gallery
Import-Module "Az"                       # Import into session
Remove-Module "Az"                       # Remove from session
Update-Module "Az"                       # Update installed module
Uninstall-Module "Az"                    # Uninstall module

# Useful built-in modules
Import-Module ActiveDirectory            # AD management
Import-Module NetAdapter                 # Network adapters
Import-Module Hyper-V                    # Virtual machines

# PSGallery — the official module repository
Register-PSRepository -Default          # Register PSGallery
Set-PSRepository -Name PSGallery -InstallationPolicy Trusted
```

---

## Remoting (PSRemoting)

**Definition:** Run PowerShell commands on remote computers using PSRemoting (WinRM).

```powershell
# Enable remoting (run as admin on target machine)
Enable-PSRemoting -Force

# Run command on remote computer
Invoke-Command -ComputerName "Server01" -ScriptBlock {
    Get-Service
}

# Run script file on remote computer
Invoke-Command -ComputerName "Server01" -FilePath "C:\script.ps1"

# Interactive remote session
Enter-PSSession -ComputerName "Server01"        # Enter session
Exit-PSSession                                   # Leave session

# Persistent session (reuse connection)
$session = New-PSSession -ComputerName "Server01"
Invoke-Command -Session $session -ScriptBlock { Get-Process }
Remove-PSSession $session                        # Close session

# Multiple computers
Invoke-Command -ComputerName "Server01", "Server02" -ScriptBlock {
    Restart-Service "Spooler"
}
```

---

## Scheduled Tasks

**Definition:** Create and manage scheduled tasks to run scripts automatically on Windows.

```powershell
# List tasks
Get-ScheduledTask                                 # All tasks
Get-ScheduledTask -TaskName "MyTask"             # Specific task

# Create a task
$action = New-ScheduledTaskAction -Execute "PowerShell.exe" `
    -Argument "-File C:\scripts\backup.ps1"

$trigger = New-ScheduledTaskTrigger -Daily -At "2:00AM"

Register-ScheduledTask -TaskName "DailyBackup" `
    -Action $action `
    -Trigger $trigger `
    -Description "Daily backup script"

# Run, stop, delete task
Start-ScheduledTask -TaskName "DailyBackup"
Stop-ScheduledTask -TaskName "DailyBackup"
Unregister-ScheduledTask -TaskName "DailyBackup" -Confirm:$false
```

---

## PowerShell Scripts (.ps1)

**Definition:** PowerShell script files use the `.ps1` extension and support full scripting with functions, error handling, and parameters.

```powershell
#!/usr/bin/env pwsh
# Script: deploy.ps1
# Description: Example deployment script
# Usage: .\deploy.ps1 -AppName "MyApp" -Environment "prod"

[CmdletBinding()]
param (
    [Parameter(Mandatory=$true)]
    [string]$AppName,

    [ValidateSet("dev", "staging", "prod")]
    [string]$Environment = "dev"
)

# Strict mode — catches common mistakes
Set-StrictMode -Version Latest
$ErrorActionPreference = "Stop"     # Stop on any error

# Logging function
function Write-Log {
    param ([string]$Message)
    $timestamp = Get-Date -Format "yyyy-MM-dd HH:mm:ss"
    Write-Output "[$timestamp] $Message"
}

Write-Log "Starting deployment of $AppName to $Environment"

try {
    # Your deployment code here
    Write-Log "Deployment complete"
}
catch {
    Write-Log "ERROR: $($_.Exception.Message)"
    exit 1
}
```

---

## Execution Policy

**Definition:** Controls which PowerShell scripts are allowed to run on the system. A security feature of Windows PowerShell.

```powershell
Get-ExecutionPolicy                     # Check current policy
Get-ExecutionPolicy -List               # Policy at each scope

# Set execution policy
Set-ExecutionPolicy RemoteSigned        # Recommended for most users
Set-ExecutionPolicy Unrestricted        # Allow all scripts
Set-ExecutionPolicy Restricted          # Block all scripts (default)
Set-ExecutionPolicy Bypass -Scope Process  # Allow for current session only
```

| Policy | Description |
|--------|-------------|
| `Restricted` | No scripts allowed (default on Windows) |
| `AllSigned` | Only signed scripts |
| `RemoteSigned` | Local scripts OK, downloaded must be signed |
| `Unrestricted` | All scripts allowed (with warnings) |
| `Bypass` | No restrictions, no warnings |

---

## Environment Variables

**Definition:** System-wide variables that store configuration values, accessible via `$env:`.

```powershell
# Access environment variables
$env:PATH                               # System PATH
$env:COMPUTERNAME                       # Computer name
$env:USERNAME                           # Current user
$env:USERPROFILE                        # User home directory (like ~)
$env:TEMP                               # Temp folder path
$env:APPDATA                            # AppData folder

# Set environment variable (current session only)
$env:MY_API_KEY = "abc123"

# Set permanently (user level)
[System.Environment]::SetEnvironmentVariable("MY_VAR", "value", "User")

# Set permanently (machine level — needs admin)
[System.Environment]::SetEnvironmentVariable("MY_VAR", "value", "Machine")

# Remove environment variable
Remove-Item Env:\MY_API_KEY

# List all environment variables
Get-ChildItem Env:
Get-Item Env:PATH
```

---

## Aliases

**Definition:** Shortcuts for longer cmdlet names. Many familiar Bash/CMD commands work in PowerShell as aliases.

```powershell
Get-Alias                               # List all aliases
Get-Alias ls                            # Find what 'ls' maps to
Get-Alias -Definition Get-ChildItem     # Find aliases for a cmdlet

# Create alias
New-Alias -Name "ll" -Value Get-ChildItem
Set-Alias -Name "np" -Value notepad

# Remove alias
Remove-Alias "ll"

# Common built-in aliases
# ls, dir, gci  → Get-ChildItem
# cd, sl        → Set-Location
# pwd, gl       → Get-Location
# cat, gc       → Get-Content
# echo, write   → Write-Output
# ps, gps       → Get-Process
# kill, spps    → Stop-Process
# rm, del, ri   → Remove-Item
# cp            → Copy-Item
# mv            → Move-Item
# mkdir         → New-Item -ItemType Directory
# clear, cls    → Clear-Host
# history, h    → Get-History
# ?             → Where-Object
# %             → ForEach-Object
```

---

## Profile & Configuration

**Definition:** PowerShell profiles are scripts that run automatically when you start a session — customize your environment here.

```powershell
# Find profile path
$PROFILE                                 # Current user, current host
$PROFILE.CurrentUserAllHosts            # Current user, all hosts
$PROFILE.AllUsersCurrentHost            # All users, current host

# Create profile if it doesn't exist
if (!(Test-Path $PROFILE)) {
    New-Item -ItemType File -Path $PROFILE -Force
}

# Edit profile
notepad $PROFILE
code $PROFILE                            # In VS Code

# Reload profile
. $PROFILE
```

**Add to your `$PROFILE`:**

```powershell
# Custom aliases
Set-Alias -Name "ll" -Value Get-ChildItem
Set-Alias -Name "np" -Value notepad

# Custom functions
function which { Get-Command $args | Select-Object -ExpandProperty Source }
function uptime { (Get-Date) - (gcim Win32_OperatingSystem).LastBootUpTime }

# Prompt customization
function prompt {
    $path = (Get-Location).Path.Replace($HOME, "~")
    "PS [$path]> "
}

# Environment variables
$env:EDITOR = "code"
```

---

## Debugging Scripts

**Definition:** Tools and techniques to find and fix errors in PowerShell scripts.

```powershell
# Syntax and strict checking
Set-StrictMode -Version Latest          # Catch undefined vars and bad syntax
$ErrorActionPreference = "Stop"         # Stop script on any error

# Trace execution
Set-PSDebug -Trace 1                    # Trace each line (level 1)
Set-PSDebug -Trace 2                    # Trace + variable assignments
Set-PSDebug -Off                        # Turn off tracing

# Verbose output
Write-Verbose "Checkpoint reached"      # Only shows with -Verbose flag
$VerbosePreference = "Continue"         # Always show verbose messages

# Debug output
Write-Debug "Value: $var"              # Only shows with -Debug flag
$DebugPreference = "Continue"          # Always show debug messages

# Breakpoints (VS Code / ISE)
Set-PSBreakpoint -Script "script.ps1" -Line 10   # Break at line 10
Get-PSBreakpoint                                  # List breakpoints
Remove-PSBreakpoint -Id 0                         # Remove breakpoint

# Common error variable
$Error[0]                              # Last error
$Error[0].Exception.Message            # Error message text
$Error[0].ScriptStackTrace             # Where it happened
$Error.Clear()                         # Clear all errors

# Check what a command does without running
Get-Command Deploy-App | Select-Object -ExpandProperty Parameters
```

---

## Shortcut Keys

**Definition:** Keyboard shortcuts for faster use in the PowerShell terminal (PSReadLine).

| Shortcut | Action |
|----------|--------|
| `Ctrl + C` | Cancel / stop current command |
| `Ctrl + L` | Clear screen |
| `Ctrl + A` | Move to start of line |
| `Ctrl + E` | Move to end of line |
| `Ctrl + R` | Reverse search history |
| `Ctrl + W` | Delete previous word |
| `Ctrl + K` | Delete to end of line |
| `Ctrl + U` | Delete to start of line |
| `Tab` | Auto-complete |
| `Ctrl + Space` | Show completion menu |
| `F7` | History popup window |
| `Up / Down` | Navigate command history |
| `Alt + .` | Insert last argument |
| `Ctrl + Z` | Undo |

---

## Tips and Tricks

**Definition:** Useful shortcuts and tricks to work more efficiently in PowerShell.

```powershell
# Run last command again
Invoke-History -Id (Get-History | Select-Object -Last 1).Id

# Quick object exploration
Get-Process | gm                    # Get-Member shorthand
Get-Process | fl *                  # Format-List all properties
Get-Process | ft -Auto              # Format-Table auto-size

# Null coalescing (PowerShell 7+)
$val = $null
$result = $val ?? "default"         # → "default"

# Null conditional (PowerShell 7+)
$obj = $null
$obj?.Name                          # No error if $obj is null

# Pipeline chain operators (PowerShell 7+)
cmd1 && cmd2    # Run cmd2 only if cmd1 succeeds
cmd1 || cmd2    # Run cmd2 only if cmd1 fails

# Measure script execution time
Measure-Command { Get-ChildItem C:\ -Recurse }

# Find what takes long
Trace-Command -Name ParameterBinding -Expression { Get-Process } -PSHost

# One-liner to find large files
Get-ChildItem C:\ -Recurse -File | Sort-Object Length -Descending | Select-Object -First 10 Name, Length

# Quick Base64 encode/decode
[Convert]::ToBase64String([Text.Encoding]::UTF8.GetBytes("Hello"))
[Text.Encoding]::UTF8.GetString([Convert]::FromBase64String("SGVsbG8="))
```

---

## Best Practices

**Definition:** Recommended guidelines for writing clean, safe, and maintainable PowerShell scripts.

```powershell
# 1. Always use CmdletBinding and param block for scripts
[CmdletBinding()]
param (
    [Parameter(Mandatory=$true)]
    [string]$InputPath
)

# 2. Set strict mode and stop on errors
Set-StrictMode -Version Latest
$ErrorActionPreference = "Stop"

# 3. Use approved Verb-Noun naming for functions
function Get-UserReport { }     # Good
function userreport { }         # Bad

# 4. Quote strings with variables
$path = "C:\Users\$env:USERNAME\Documents"   # Good — interpolates
$path = 'C:\Users\$env:USERNAME\Documents'   # Bad — literal $env

# 5. Use full cmdlet names in scripts (not aliases)
Get-ChildItem     # Good — clear and readable
ls                # Bad in scripts — unclear to others

# 6. Use -WhatIf and -Confirm for destructive operations
function Remove-OldLogs {
    [CmdletBinding(SupportsShouldProcess=$true)]
    param ([string]$Path)

    if ($PSCmdlet.ShouldProcess($Path, "Remove")) {
        Remove-Item $Path
    }
}

# 7. Always validate parameters
[ValidateNotNullOrEmpty()]
[string]$Name

# 8. Use Write-Verbose for diagnostic info
Write-Verbose "Processing file: $file"       # Hidden by default

# 9. Prefer CIM over WMI
Get-CimInstance Win32_Process    # Good — modern
Get-WmiObject Win32_Process      # Old — deprecated in PS 7+

# 10. Comment your code
# Good comment: explains WHY, not what
$retries = 3    # Retry up to 3 times to handle transient network errors
```

**Summary of rules:**

* Use `[CmdletBinding()]` and `param()` in every script
* Always set `Set-StrictMode -Version Latest`
* Use `$ErrorActionPreference = "Stop"` to catch errors early
* Use full cmdlet names, not aliases, in scripts
* Validate all parameters with `[Parameter()]` attributes
* Use `Write-Verbose` / `Write-Debug` instead of `Write-Host` for logging
* Support `-WhatIf` for any destructive operations
* Use `try/catch/finally` for error handling
* Prefer `Get-CimInstance` over `Get-WmiObject`
* Test scripts with `-WhatIf` before running destructively
