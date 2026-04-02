# Nmap Cheat Sheet

## Introduction

**Nmap** (Network Mapper) is a free, open-source network discovery and security auditing tool created by **Gordon Lyon (Fyodor)** and released in **1997**. Nmap uses raw IP packets to determine what hosts are available on a network, what services they are running, what operating systems they use, what firewalls are in place, and many other characteristics. It is widely used by **network administrators**, **penetration testers**, and **security researchers**. Nmap can scan a single host or an entire enterprise network. It supports dozens of scan techniques and runs on Linux, Windows, and macOS. Always obtain **written permission** before scanning any network you do not own.

> ⚠️ **Legal Warning:** Unauthorized scanning is illegal in many jurisdictions. Always have explicit written permission before scanning any network or system you do not own.

---

## Table of Contents

1. [Basic Usage](#basic-usage)
2. [Target Specification](#target-specification)
3. [Host Discovery](#host-discovery)
4. [Port Specification](#port-specification)
5. [Scan Techniques](#scan-techniques)
6. [Service & Version Detection](#service--version-detection)
7. [OS Detection](#os-detection)
8. [Timing & Performance](#timing--performance)
9. [Firewall & IDS Evasion](#firewall--ids-evasion)
10. [Output Formats](#output-formats)
11. [Nmap Scripting Engine (NSE)](#nmap-scripting-engine-nse)
12. [NSE Script Categories](#nse-script-categories)
13. [Useful NSE Scripts](#useful-nse-scripts)
14. [IPv6 Scanning](#ipv6-scanning)
15. [Nmap with Proxies & Tor](#nmap-with-proxies--tor)
16. [Ndiff — Compare Scans](#ndiff--compare-scans)
17. [Zenmap — GUI Frontend](#zenmap--gui-frontend)
18. [Common Scan Profiles](#common-scan-profiles)
19. [Reading Nmap Output](#reading-nmap-output)
20. [Tips & Tricks](#tips--tricks)
21. [Best Practices](#best-practices)

---

## Basic Usage

**Definition:** Nmap's most fundamental commands — run as root/sudo for most scan types to access raw sockets.

### Simple Scan
**Definition:** The most basic Nmap scan — scans the 1000 most common ports on a target.
```bash
nmap 192.168.1.1                # Scan a single IP
nmap example.com                # Scan a hostname
nmap 192.168.1.1 192.168.1.2   # Scan multiple IPs
nmap -v 192.168.1.1             # Verbose output
nmap -vv 192.168.1.1            # Very verbose output
```

### Installation
**Definition:** Install Nmap on different operating systems.
```bash
# Ubuntu / Debian
sudo apt install nmap

# CentOS / RHEL / Fedora
sudo yum install nmap
sudo dnf install nmap

# macOS (Homebrew)
brew install nmap

# Windows
# Download installer from https://nmap.org/download.html

# Verify installation
nmap --version
nmap -V
```

### Getting Help
**Definition:** Access built-in help and documentation.
```bash
nmap -h                         # Quick help summary
man nmap                        # Full man page
nmap --help                     # Detailed help
```

---

## Target Specification

**Definition:** Tell Nmap what to scan — single hosts, ranges, subnets, or lists from files.

### Single Targets
**Definition:** Scan one host at a time using IP address, hostname, or CIDR notation.
```bash
nmap 192.168.1.1                # Single IP address
nmap 10.0.0.1                   # Single IP address
nmap example.com                # Hostname — resolved to IP
nmap www.example.com            # Subdomain
```

### Multiple & Range Targets
**Definition:** Scan multiple hosts or ranges in one command.
```bash
nmap 192.168.1.1 192.168.1.2 192.168.1.3   # Multiple IPs (space-separated)
nmap 192.168.1.1,2,3                        # Multiple IPs (comma notation)
nmap 192.168.1.1-20                         # IP range: .1 to .20
nmap 192.168.1-5.1-254                      # Multiple octet ranges
nmap 192.168.1.*                            # Wildcard — all 256 hosts in subnet
```

### Subnet / CIDR Notation
**Definition:** Scan entire networks using CIDR subnet notation.
```bash
nmap 192.168.1.0/24             # /24 = 256 addresses (192.168.1.0 to .255)
nmap 10.0.0.0/8                 # /8  = 16 million addresses
nmap 172.16.0.0/16              # /16 = 65536 addresses
nmap 192.168.0.0/16             # Large class B network
```

### Input from File
**Definition:** Read targets from a text file — one target per line.
```bash
nmap -iL targets.txt            # Scan all targets listed in file
nmap -iL /path/to/hosts.txt     # With full path

# targets.txt format:
# 192.168.1.1
# 192.168.1.0/24
# example.com
# 10.0.0.1-50
```

### Exclude Targets
**Definition:** Skip specific hosts or networks from a scan.
```bash
nmap 192.168.1.0/24 --exclude 192.168.1.1         # Exclude one IP
nmap 192.168.1.0/24 --exclude 192.168.1.1,192.168.1.2  # Exclude multiple
nmap 192.168.1.0/24 --excludefile exclude.txt     # Exclude from file
nmap 192.168.1.0/24 --exclude 192.168.1.0/28      # Exclude a subnet
```

### Random Targets
**Definition:** Scan random internet hosts — requires permission, for research only.
```bash
nmap -iR 10                     # Scan 10 random internet hosts
nmap -iR 100 -p 80              # 100 random hosts on port 80
nmap -iR 0                      # Infinite random scan (run forever)
```

---

## Host Discovery

**Definition:** Determine which hosts in a range are online before scanning their ports.

### Ping Scan (No Port Scan)
**Definition:** Discover live hosts without scanning ports — fast way to map a network.
```bash
nmap -sn 192.168.1.0/24         # Ping scan — host discovery only, no ports
nmap -sP 192.168.1.0/24         # Older syntax — same as -sn
```

### Skip Host Discovery
**Definition:** Assume all hosts are up — useful when hosts block ping but have open ports.
```bash
nmap -Pn 192.168.1.1            # Skip ping — treat all hosts as up
nmap -Pn 192.168.1.0/24         # No ping, scan all ports on all hosts
```

### Discovery Methods
**Definition:** Different techniques Nmap uses to determine if a host is alive.
```bash
nmap -PS 192.168.1.1            # TCP SYN ping (default port 80)
nmap -PS22,80,443 192.168.1.1   # TCP SYN ping to specific ports
nmap -PA 192.168.1.1            # TCP ACK ping
nmap -PA22,80,443 192.168.1.1   # TCP ACK ping to specific ports
nmap -PU 192.168.1.1            # UDP ping
nmap -PU53,161 192.168.1.1      # UDP ping to specific ports
nmap -PY 192.168.1.1            # SCTP INIT ping
nmap -PE 192.168.1.1            # ICMP Echo Request ping
nmap -PP 192.168.1.1            # ICMP Timestamp ping
nmap -PM 192.168.1.1            # ICMP Netmask ping
nmap -PO 192.168.1.1            # IP Protocol ping
```

### ARP Scan (LAN Only)
**Definition:** Use ARP for host discovery on local networks — much faster and more reliable than ICMP.
```bash
nmap -PR 192.168.1.0/24         # ARP scan — only works on local subnet
sudo nmap -PR 192.168.1.0/24    # Root required for ARP
```

### DNS Options
**Definition:** Control how Nmap resolves hostnames.
```bash
nmap -n 192.168.1.0/24          # No DNS resolution — faster scans
nmap -R 192.168.1.0/24          # Always resolve DNS (default: only live hosts)
nmap --dns-servers 8.8.8.8 target  # Use specific DNS server
nmap --system-dns target         # Use OS DNS resolver
```

---

## Port Specification

**Definition:** Control which ports Nmap scans — by number, range, name, or state.

### Specific Ports
**Definition:** Scan exact ports by number or service name.
```bash
nmap -p 80 192.168.1.1                  # Single port 80
nmap -p 80,443 192.168.1.1              # Two specific ports
nmap -p 80,443,8080,8443 192.168.1.1   # Multiple specific ports
nmap -p 22-100 192.168.1.1             # Port range 22 to 100
nmap -p 1-1000 192.168.1.1             # Range 1-1000
nmap -p http,ftp,ssh 192.168.1.1       # By service name
nmap -p T:80,U:53 192.168.1.1          # T: for TCP, U: for UDP
```

### Port Ranges
**Definition:** Scan large ranges or all 65535 ports.
```bash
nmap -p- 192.168.1.1                    # ALL 65535 ports (1-65535)
nmap -p 1-65535 192.168.1.1            # Same — all ports
nmap -p 0- 192.168.1.1                 # Ports 0 through 65535 (includes port 0)
nmap --top-ports 10 192.168.1.1        # Top 10 most common ports
nmap --top-ports 100 192.168.1.1       # Top 100 most common ports
nmap --top-ports 1000 192.168.1.1      # Top 1000 (default)
```

### Port Selection Options
**Definition:** Additional options for controlling which ports to scan.
```bash
nmap -F 192.168.1.1                     # Fast scan — top 100 ports only
nmap -r 192.168.1.1                     # Scan ports in sequential order
nmap --port-ratio 0.1 192.168.1.1      # Ports appearing in >10% of scans
```

---

## Scan Techniques

**Definition:** Different methods for probing ports — each behaves differently and has different detection characteristics.

### TCP Scan Types
**Definition:** Methods for scanning TCP ports — SYN is the fastest and most reliable.
```bash
nmap -sS 192.168.1.1            # TCP SYN scan (Half-open) — default, fast, stealthy
nmap -sT 192.168.1.1            # TCP Connect scan — full 3-way handshake, logged
nmap -sA 192.168.1.1            # TCP ACK scan — map firewall rules, not port state
nmap -sW 192.168.1.1            # TCP Window scan — like ACK but checks window size
nmap -sM 192.168.1.1            # TCP Maimon scan — FIN/ACK probe
nmap -sN 192.168.1.1            # TCP Null scan — no flags set
nmap -sF 192.168.1.1            # TCP FIN scan — only FIN flag
nmap -sX 192.168.1.1            # TCP Xmas scan — FIN, PSH, URG flags
```

### UDP Scan
**Definition:** Scan UDP ports — slower than TCP because UDP is connectionless.
```bash
nmap -sU 192.168.1.1            # UDP scan — slow but important
nmap -sU -p 53,67,68,161,162 192.168.1.1  # Common UDP ports
nmap -sU --top-ports 20 192.168.1.1       # Top 20 UDP ports
nmap -sU -sS 192.168.1.1        # Combine UDP and TCP SYN scan
```

### SCTP Scan Types
**Definition:** Scan SCTP (Stream Control Transmission Protocol) ports.
```bash
nmap -sY 192.168.1.1            # SCTP INIT scan
nmap -sZ 192.168.1.1            # SCTP COOKIE-ECHO scan
```

### Other Protocols
**Definition:** Scan for other IP protocols beyond TCP, UDP, and SCTP.
```bash
nmap -sO 192.168.1.1            # IP Protocol scan — which IP protocols supported
```

### Port States Explained
**Definition:** The six states Nmap reports for scanned ports.

| State | Meaning |
|-------|---------|
| `open` | Application is actively accepting connections |
| `closed` | Port is accessible but no application is listening |
| `filtered` | Firewall is blocking the probe — state unknown |
| `unfiltered` | Port accessible but Nmap can't determine open/closed |
| `open\|filtered` | Cannot determine if open or filtered |
| `closed\|filtered` | Cannot determine if closed or filtered |

---

## Service & Version Detection

**Definition:** Identify the application name and version running on open ports.

### Version Scanning
**Definition:** Probe open ports to determine the exact service and version running.
```bash
nmap -sV 192.168.1.1                    # Service version detection
nmap -sV --version-intensity 0 target   # Lightest probing (fastest)
nmap -sV --version-intensity 5 target   # Default intensity
nmap -sV --version-intensity 9 target   # Maximum probing (most intrusive)
nmap -sV --version-all target           # Try all probes — most thorough
nmap -sV --version-light target         # Light — fewer probes, faster
```

### Version Detection Output
**Definition:** Example output from version detection and what it means.
```
PORT     STATE SERVICE  VERSION
22/tcp   open  ssh      OpenSSH 8.9 (protocol 2.0)
80/tcp   open  http     Apache httpd 2.4.52 ((Ubuntu))
443/tcp  open  ssl/http Apache httpd 2.4.52 ((Ubuntu))
3306/tcp open  mysql    MySQL 8.0.30
```

---

## OS Detection

**Definition:** Identify the operating system and hardware running on target hosts.

### OS Detection Options
**Definition:** Probe targets to fingerprint their OS by analyzing TCP/IP stack behavior.
```bash
nmap -O 192.168.1.1             # OS detection
nmap -O --osscan-guess target   # Guess OS if no perfect match
nmap -O --osscan-limit target   # Only detect OS on promising targets
nmap -O --fuzzy target          # Same as --osscan-guess
```

### Combined Detection
**Definition:** Run OS and version detection together — most useful combination.
```bash
nmap -sV -O 192.168.1.1         # Version + OS detection
nmap -A 192.168.1.1             # Aggressive: -sV -O + traceroute + NSE scripts
```

### OS Detection Output
**Definition:** Example of OS detection results.
```
OS details: Linux 4.15 - 5.6
Network Distance: 1 hop

OS CPE: cpe:/o:linux:linux_kernel:5

Running: Linux 5.X
OS CPE: cpe:/o:linux:linux_kernel:5
OS details: Linux 5.0 - 5.4
Uptime guess: 2.150 days (since Fri Jan 13 09:30:00 2025)
```

---

## Timing & Performance

**Definition:** Control how fast Nmap scans — balance speed against accuracy and stealth.

### Timing Templates
**Definition:** Six predefined timing profiles from paranoid (slowest) to insane (fastest).
```bash
nmap -T0 192.168.1.1            # Paranoid  — very slow, evades IDS, 5 min delay
nmap -T1 192.168.1.1            # Sneaky    — slow, evades IDS, 15 sec delay
nmap -T2 192.168.1.1            # Polite    — slower, less bandwidth
nmap -T3 192.168.1.1            # Normal    — default timing
nmap -T4 192.168.1.1            # Aggressive — faster, assumes good network
nmap -T5 192.168.1.1            # Insane    — very fast, may miss ports
```

| Template | Name | Use Case |
|----------|------|---------|
| `-T0` | Paranoid | IDS evasion, very slow |
| `-T1` | Sneaky | IDS evasion, slow |
| `-T2` | Polite | Low bandwidth, slow |
| `-T3` | Normal | Default — balanced |
| `-T4` | Aggressive | Fast networks, CTF, labs |
| `-T5` | Insane | Fastest, may miss ports |

### Fine-Tuned Timing
**Definition:** Override specific timing parameters for custom control.
```bash
nmap --min-rate 100 target          # Send at least 100 packets/sec
nmap --max-rate 200 target          # Send at most 200 packets/sec
nmap --min-parallelism 10 target    # At least 10 probes in parallel
nmap --max-parallelism 100 target   # At most 100 probes in parallel
nmap --min-hostgroup 5 target       # Scan at least 5 hosts simultaneously
nmap --max-hostgroup 20 target      # Scan at most 20 hosts simultaneously
nmap --host-timeout 30m target      # Give up on host after 30 minutes
nmap --scan-delay 1s target         # Wait 1 second between probes
nmap --max-scan-delay 5s target     # Maximum delay between probes
nmap --max-retries 3 target         # Max port scan probe retransmissions
nmap --min-rtt-timeout 100ms target # Minimum round-trip time
nmap --max-rtt-timeout 3000ms target # Maximum round-trip time
nmap --initial-rtt-timeout 500ms target # Starting RTT timeout
```

---

## Firewall & IDS Evasion

**Definition:** Techniques to avoid detection by firewalls, intrusion detection systems (IDS), and packet filters.

### Fragmentation
**Definition:** Split packets into small fragments that some firewalls can't reassemble.
```bash
nmap -f target                  # Fragment packets (8 bytes per fragment)
nmap -ff target                 # Double fragmentation (16 bytes)
nmap --mtu 16 target            # Set custom MTU (must be multiple of 8)
nmap --mtu 24 target
nmap --mtu 32 target
```

### Decoys
**Definition:** Spoof scan traffic to appear to come from multiple sources — hides real scanner.
```bash
nmap -D RND:5 target            # Use 5 random decoy IPs
nmap -D 10.0.0.1,10.0.0.2,ME target  # Specific decoys (ME = real IP)
nmap -D 10.0.0.1,10.0.0.2,10.0.0.3 target  # Three decoys, real IP hidden
```

### Source Spoofing
**Definition:** Spoof the source address — replies go to the spoofed address, not you.
```bash
nmap -S 10.0.0.100 target       # Spoof source IP address
nmap -e eth0 target             # Use specific network interface
nmap -g 53 target               # Use port 53 as source port (looks like DNS)
nmap --source-port 53 target    # Same — specify source port
nmap --spoof-mac 0 target       # Random spoofed MAC address
nmap --spoof-mac Dell target    # Spoof MAC from Dell vendor
nmap --spoof-mac AA:BB:CC:DD:EE:FF target  # Specific MAC address
```

### Timing Evasion
**Definition:** Slow down scans to avoid triggering rate-based IDS rules.
```bash
nmap -T0 target                 # Paranoid — 5 min between probes
nmap -T1 target                 # Sneaky — 15 sec between probes
nmap --scan-delay 5s target     # 5 second delay between probes
nmap --max-rate 10 target       # Max 10 packets per second
```

### Packet Manipulation
**Definition:** Alter packet characteristics to bypass filters.
```bash
nmap --data-length 25 target    # Append 25 random bytes to packets
nmap --ip-options "" target     # Set IP options
nmap --ttl 64 target            # Set TTL value
nmap --badsum target            # Send packets with invalid checksums
```

---

## Output Formats

**Definition:** Save scan results to different file formats for reporting and analysis.

### Output Options
**Definition:** Save results during scanning — multiple formats can be saved simultaneously.
```bash
nmap -oN output.txt target      # Normal output (human-readable)
nmap -oX output.xml target      # XML output (for parsers)
nmap -oG output.gnmap target    # Grepable output (for grep/awk)
nmap -oJ output.json target     # JSON output (Nmap 7.93+)
nmap -oS output.txt target      # Script kiddie output (leet speak — joke)
nmap -oA output target          # All formats — saves .nmap, .xml, .gnmap

# Append to existing file
nmap -oN - target               # Output to stdout (normal format)
nmap -oN output.txt --append-output target  # Append to file
```

### Verbose & Debug
**Definition:** Increase output detail during and after scanning.
```bash
nmap -v target                  # Verbose — show open ports in real-time
nmap -vv target                 # Very verbose
nmap -vvv target                # Maximum verbosity
nmap -d target                  # Debug level 1
nmap -dd target                 # Debug level 2
nmap --reason target            # Show reason port is in each state
nmap --packet-trace target      # Show all sent/received packets (very verbose)
nmap --open target              # Show only open ports
nmap --iflist                   # List network interfaces and routes
```

### Resume Interrupted Scans
**Definition:** Continue a scan that was interrupted.
```bash
nmap --resume output.gnmap      # Resume from grepable output file
nmap --resume output.xml        # Resume from XML output file
```

---

## Nmap Scripting Engine (NSE)

**Definition:** Built-in Lua scripting engine — runs scripts to detect vulnerabilities, gather information, and automate tasks.

### Run Scripts
**Definition:** Execute NSE scripts during scanning — scripts extend Nmap's capabilities massively.
```bash
nmap -sC target                 # Run default scripts (same as --script=default)
nmap --script=default target    # Run default category scripts
nmap --script=banner target     # Run specific script
nmap --script=http-title target # Get HTTP page titles
nmap --script="http-*" target   # All scripts starting with "http-"
nmap --script=vuln target       # Run all vulnerability scripts
nmap --script=safe target       # Run all safe scripts
```

### Script Arguments
**Definition:** Pass arguments to NSE scripts that require configuration.
```bash
nmap --script=http-brute --script-args userdb=users.txt,passdb=pass.txt target
nmap --script=smb-brute --script-args smbuser=admin target
nmap --script=ftp-anon --script-args ftp.passive=true target
nmap --script=http-put --script-args http-put.url="/test",http-put.file=file.txt target
```

### Script Management
**Definition:** Update, search, and manage the NSE script library.
```bash
nmap --script-updatedb           # Update script database
nmap --script-help http-title    # Show help for a specific script
nmap --script-help "http-*"      # Show help for script pattern
ls /usr/share/nmap/scripts/      # List all scripts (Linux)
nmap --script-args-file args.txt target  # Load args from file
```

---

## NSE Script Categories

**Definition:** Scripts are organized into categories — run entire categories or mix and match.

### Category Reference
**Definition:** The official NSE script categories and what each contains.

| Category | Description |
|----------|-------------|
| `auth` | Authentication bypass and credential checking |
| `broadcast` | Host discovery via broadcast messages |
| `brute` | Brute-force authentication attacks |
| `default` | Safe, useful scripts run with `-sC` |
| `discovery` | Service and host discovery |
| `dos` | Denial of service testing — use carefully |
| `exploit` | Exploit known vulnerabilities |
| `external` | Scripts calling external resources |
| `fuzzer` | Fuzzing — send unusual data to services |
| `intrusive` | Likely to crash services or cause alerts |
| `malware` | Detect backdoors and malware |
| `safe` | Non-intrusive, safe to run on any host |
| `version` | Supplement version detection |
| `vuln` | Detect known security vulnerabilities |

```bash
nmap --script=auth target       # Authentication scripts
nmap --script=brute target      # Brute force scripts
nmap --script=default target    # Default safe scripts
nmap --script=discovery target  # Discovery scripts
nmap --script=exploit target    # Exploitation scripts
nmap --script=vuln target       # Vulnerability detection scripts
nmap --script=safe target       # All safe scripts
nmap --script=intrusive target  # Intrusive scripts — may cause issues!

# Combine categories
nmap --script="default,safe" target
nmap --script="vuln and safe" target
nmap --script="not intrusive" target
```

---

## Useful NSE Scripts

**Definition:** Commonly used individual scripts for specific tasks — run with `--script=scriptname`.

### HTTP Scripts
**Definition:** Gather information about web services running on target.
```bash
nmap --script=http-title -p 80,443 target       # Get web page titles
nmap --script=http-headers -p 80,443 target     # Show HTTP response headers
nmap --script=http-methods -p 80,443 target     # List allowed HTTP methods
nmap --script=http-robots.txt -p 80 target      # Get robots.txt contents
nmap --script=http-auth -p 80 target            # Test for HTTP auth
nmap --script=http-shellshock target            # Test for Shellshock (CVE-2014-6271)
nmap --script=http-sql-injection target         # Test for SQL injection
nmap --script=http-xssed target                 # Check XSSed.com database
nmap --script=http-open-redirect target         # Detect open redirects
nmap --script=http-wordpress-users target       # Enumerate WordPress users
nmap --script=http-enum target                  # Enumerate web directories
nmap --script=http-sitemap-generator target     # Generate sitemap
```

### SSH Scripts
**Definition:** Discover SSH service information and test authentication.
```bash
nmap --script=ssh-hostkey -p 22 target          # Get SSH host keys
nmap --script=ssh-auth-methods -p 22 target     # List SSH auth methods
nmap --script=ssh-brute -p 22 target            # Brute force SSH
nmap --script=ssh2-enum-algos -p 22 target      # List SSH algorithms
nmap --script=sshv1 -p 22 target                # Check if SSHv1 enabled
```

### SMB Scripts (Windows)
**Definition:** Gather information about Windows SMB/Samba services.
```bash
nmap --script=smb-os-discovery -p 445 target    # Get OS via SMB
nmap --script=smb-enum-users -p 445 target      # Enumerate SMB users
nmap --script=smb-enum-shares -p 445 target     # List SMB shares
nmap --script=smb-vuln-ms17-010 -p 445 target   # EternalBlue (MS17-010)
nmap --script=smb-vuln-ms08-067 -p 445 target   # MS08-067 vulnerability
nmap --script=smb-brute -p 445 target           # Brute force SMB
nmap --script=smb-security-mode -p 445 target   # SMB security settings
nmap --script="smb-vuln-*" -p 445 target        # All SMB vulnerabilities
```

### FTP Scripts
**Definition:** Test FTP services for common misconfigurations.
```bash
nmap --script=ftp-anon -p 21 target             # Test for anonymous FTP login
nmap --script=ftp-bounce -p 21 target           # Test for FTP bounce attack
nmap --script=ftp-brute -p 21 target            # Brute force FTP
nmap --script=ftp-syst -p 21 target             # Get FTP system type
nmap --script=ftp-vsftpd-backdoor -p 21 target  # Test for vsftpd backdoor
```

### Database Scripts
**Definition:** Probe and enumerate database services.
```bash
nmap --script=mysql-info -p 3306 target         # MySQL server info
nmap --script=mysql-empty-password -p 3306 target  # Test empty root password
nmap --script=mysql-users -p 3306 target        # Enumerate MySQL users
nmap --script=mysql-brute -p 3306 target        # Brute force MySQL
nmap --script=ms-sql-info -p 1433 target        # MSSQL server info
nmap --script=ms-sql-brute -p 1433 target       # Brute force MSSQL
nmap --script=mongodb-info -p 27017 target      # MongoDB info
nmap --script=redis-info -p 6379 target         # Redis server info
nmap --script=oracle-brute -p 1521 target       # Brute force Oracle DB
```

### SNMP Scripts
**Definition:** Query SNMP services for system information.
```bash
nmap --script=snmp-info -p 161 target           # SNMP basic info
nmap --script=snmp-sysdescr -p 161 target       # System description
nmap --script=snmp-interfaces -p 161 target     # Network interfaces
nmap --script=snmp-processes -p 161 target      # Running processes
nmap --script=snmp-netstat -p 161 target        # Network connections
nmap --script=snmp-brute -p 161 target          # Brute force community strings
```

### SSL/TLS Scripts
**Definition:** Test SSL/TLS configuration and find vulnerabilities.
```bash
nmap --script=ssl-cert -p 443 target            # Get SSL certificate info
nmap --script=ssl-enum-ciphers -p 443 target    # List supported SSL/TLS ciphers
nmap --script=ssl-heartbleed -p 443 target      # Test for Heartbleed (CVE-2014-0160)
nmap --script=ssl-poodle -p 443 target          # Test for POODLE vulnerability
nmap --script=ssl-dh-params -p 443 target       # Detect weak DH params (Logjam)
nmap --script=sslv2 -p 443 target               # Check if SSLv2 enabled
```

### DNS Scripts
**Definition:** Enumerate and test DNS services.
```bash
nmap --script=dns-brute target                  # Brute force DNS subdomains
nmap --script=dns-zone-transfer -p 53 target    # Test for DNS zone transfer
nmap --script=dns-recursion -p 53 target        # Test for open DNS recursion
nmap --script=dns-cache-snoop -p 53 target      # DNS cache snooping
```

### Vulnerability Scripts
**Definition:** Test for common CVEs and security vulnerabilities.
```bash
nmap --script=vuln target                       # Run all vuln scripts
nmap --script=vuln -p 445 target               # Vuln scripts for SMB
nmap --script=vulscan --script-args vulscandb=scipvuldb.csv target  # Vulscan plugin
```

---

## IPv6 Scanning

**Definition:** Scan IPv6 targets — requires the `-6` flag.

### IPv6 Options
**Definition:** Enable IPv6 scanning for modern networks.
```bash
nmap -6 ::1                     # Scan IPv6 loopback
nmap -6 2001:db8::1             # Scan specific IPv6 address
nmap -6 fe80::1%eth0            # Scan link-local address
nmap -6 --script ipv6-node-info 2001:db8::1  # IPv6 node info script
```

---

## Nmap with Proxies & Tor

**Definition:** Route Nmap scans through proxies or Tor — for anonymity or testing internal networks.

### Proxychains
**Definition:** Route TCP scans through SOCKS4/SOCKS5 proxies using proxychains.
```bash
proxychains nmap -sT -Pn 192.168.1.1       # Route through Tor (proxychains + Tor)
proxychains nmap -sT -n -Pn target         # Must use -sT (TCP connect) with proxychains
proxychains4 nmap -sT -Pn target           # Newer proxychains4 command
```

### Ncat / Proxy Options
**Definition:** Configure proxy settings directly in Nmap.
```bash
nmap --proxies socks4://127.0.0.1:9050 target    # SOCKS4 proxy (Tor)
nmap --proxies socks5://127.0.0.1:9050 target    # SOCKS5 proxy (Tor)
nmap --proxies http://proxy:8080 target           # HTTP proxy
```

---

## Ndiff — Compare Scans

**Definition:** Ndiff compares two Nmap XML output files to show what changed between scans.

### Ndiff Usage
**Definition:** Detect new open ports, closed services, and OS changes over time.
```bash
ndiff scan1.xml scan2.xml               # Compare two scans
ndiff --text scan1.xml scan2.xml        # Text format output
ndiff --xml scan1.xml scan2.xml         # XML format output
ndiff -v scan1.xml scan2.xml            # Verbose comparison

# Workflow: save XML, scan again later, compare
nmap -oX scan_monday.xml 192.168.1.0/24
# ... (scan again on Friday)
nmap -oX scan_friday.xml 192.168.1.0/24
ndiff scan_monday.xml scan_friday.xml   # See what changed
```

---

## Zenmap — GUI Frontend

**Definition:** Zenmap is the official graphical interface for Nmap — good for beginners and visualization.

### Zenmap Features
**Definition:** A visual way to run Nmap scans with profile management and topology mapping.
```bash
zenmap                          # Launch Zenmap GUI
zenmap -p "Intense scan" target # Launch with a specific profile

# Built-in Zenmap profiles:
# Intense scan:        nmap -T4 -A -v target
# Intense scan + UDP:  nmap -sS -sU -T4 -A -v target
# Ping scan:           nmap -sn target
# Quick scan:          nmap -T4 -F target
# Quick scan plus:     nmap -sV -T4 -O -F --version-light target
# Quick traceroute:    nmap -sn --traceroute target
# Regular scan:        nmap target
# Slow comprehensive:  nmap -sS -sU -T4 -A -v -PE -PP -PS80,443 -PA3389 -PU40125 -PY -g 53 target
```

---

## Common Scan Profiles

**Definition:** Ready-to-use scan combinations for common penetration testing scenarios.

### Quick Discovery
**Definition:** Fast scans to map a network and identify live hosts.
```bash
# Fast host discovery — which IPs are alive
nmap -sn 192.168.1.0/24

# Quick scan of common ports
nmap -T4 -F 192.168.1.0/24

# Quick with version detection
nmap -T4 -F -sV 192.168.1.1
```

### Standard Reconnaissance
**Definition:** Balanced scans for thorough information gathering.
```bash
# Standard comprehensive scan
nmap -sV -sC -O 192.168.1.1

# Scan all ports with version detection
nmap -p- -sV 192.168.1.1

# Aggressive scan (fast, noisy)
nmap -A -T4 192.168.1.1

# Full scan with scripts and output saved
nmap -A -p- -T4 -oA full_scan 192.168.1.1
```

### Stealthy Scanning
**Definition:** Low-noise scans for red team engagements.
```bash
# Slow stealthy scan
nmap -sS -T2 -Pn 192.168.1.1

# Fragment packets for evasion
nmap -sS -f -Pn 192.168.1.1

# Paranoid timing with decoys
nmap -sS -T0 -D RND:5 192.168.1.1

# Change source port to avoid filters
nmap -sS -g 53 192.168.1.1
```

### Vulnerability Scanning
**Definition:** Scan for known security vulnerabilities.
```bash
# Run all vuln scripts
nmap -sV --script=vuln 192.168.1.1

# SMB vulnerabilities (Windows targets)
nmap -sV --script="smb-vuln-*" -p 445 192.168.1.1

# Web vulnerabilities
nmap -sV --script="http-vuln-*,http-sql-injection" -p 80,443 192.168.1.1

# All SSL/TLS issues
nmap -sV --script="ssl-*" -p 443 192.168.1.1
```

### Web Application Scanning
**Definition:** Focused scans for web servers and applications.
```bash
# Web server enumeration
nmap -sV -p 80,443,8080,8443 --script="http-*" 192.168.1.1

# Find hidden paths and directories
nmap -p 80 --script=http-enum 192.168.1.1

# Full web scan
nmap -sV -p 80,443 \
  --script=http-title,http-headers,http-methods,http-auth,http-robots.txt \
  192.168.1.1
```

### Full Penetration Test Scan
**Definition:** Comprehensive scan used in penetration testing engagements.
```bash
# Phase 1: Host discovery
nmap -sn 192.168.1.0/24 -oG hosts.gnmap

# Phase 2: Quick port scan
nmap -p- --min-rate 5000 -T4 192.168.1.1 -oN ports.txt

# Phase 3: Detailed service scan
nmap -sV -sC -O -p 22,80,443 192.168.1.1 -oA detailed

# Phase 4: Vulnerability scan
nmap --script=vuln -p 22,80,443 192.168.1.1 -oN vulns.txt
```

---

## Reading Nmap Output

**Definition:** Understand and interpret the information Nmap returns.

### Sample Output Explained
**Definition:** Full annotated Nmap output with every field explained.
```
Starting Nmap 7.93 ( https://nmap.org ) at 2025-01-15 10:30 IST
Nmap scan report for 192.168.1.1                ← Target IP or hostname
Host is up (0.0012s latency).                   ← Host is alive, RTT shown
Not shown: 995 closed tcp ports (reset)         ← 995 ports responded with RST
PORT      STATE    SERVICE    VERSION
22/tcp    open     ssh        OpenSSH 8.9 (protocol 2.0)
│                             ↑port  ↑state ↑service ↑version (with -sV)
80/tcp    open     http       Apache httpd 2.4.52
443/tcp   open     ssl/https  Apache httpd 2.4.52
3306/tcp  filtered mysql                        ← Firewall blocking this port
8080/tcp  closed   http-proxy                  ← Port accessible, nothing listening

MAC Address: 00:50:56:C0:00:08 (VMware)        ← MAC + vendor (local hosts only)
Device type: general purpose
Running: Linux 5.X                              ← OS detection result (-O)
OS CPE: cpe:/o:linux:linux_kernel:5
OS details: Linux 5.0 - 5.4
Network Distance: 1 hop                        ← Number of hops away

TRACEROUTE
HOP  RTT     ADDRESS
1    1.12 ms 192.168.1.1                       ← Traceroute path

Nmap done: 1 IP address (1 host up) scanned in 12.34 seconds
```

### Grepable Output Format
**Definition:** The `-oG` format is designed for grep, awk, and shell scripting.
```bash
# Grepable output looks like:
# Host: 192.168.1.1 ()  Status: Up
# Host: 192.168.1.1 ()  Ports: 22/open/tcp//ssh//OpenSSH 8.9/, 80/open/tcp//http//Apache 2.4.52/

# Extract open ports from grepable output
grep "open" output.gnmap
grep "/open/" output.gnmap | awk '{print $2}'

# Extract hosts with specific open port
grep "80/open" output.gnmap | awk '{print $2}'

# Extract all open ports
grep -oP '\d+/open' output.gnmap | cut -d'/' -f1 | sort -u
```

---

## Tips & Tricks

**Definition:** Practical shortcuts and techniques for effective Nmap usage.

### Useful Combinations
**Definition:** Powerful command combinations for common tasks.
```bash
# Find all web servers in a network
nmap -p 80,443,8080,8443 --open 192.168.1.0/24

# Scan specific ports fast with version
nmap -sV -p 22,80,443,3306 --open -T4 192.168.1.0/24

# Get all hostnames in a subnet
nmap -sn -R 192.168.1.0/24

# Find all SSH servers
nmap -p 22 --open 192.168.1.0/24

# Quick scan and save all formats
nmap -A -T4 192.168.1.1 -oA results/target_scan

# Scan list and show only open ports
nmap --open -iL targets.txt -oN open_ports.txt

# Find hosts with a specific service
nmap -sV -p 3306 --open 192.168.1.0/24 | grep mysql

# Combine all NSE info gathering
nmap -sV -sC --script=safe -p- -T4 192.168.1.1

# Banner grabbing
nmap -sV --script=banner -p- 192.168.1.1

# Find all open ports then deep scan those only
ports=$(nmap -p- --min-rate 5000 -T4 192.168.1.1 | grep "^[0-9]" | cut -d'/' -f1 | tr '\n' ',')
nmap -sV -sC -O -p $ports 192.168.1.1
```

### Extract & Parse Results
**Definition:** Process Nmap output with shell commands.
```bash
# Extract open ports from normal output
grep "open" output.nmap | awk '{print $1}'

# Count open ports
grep -c "open" output.nmap

# List unique services found
grep "open" output.nmap | awk '{print $3}' | sort -u

# Convert XML to readable report
xsltproc nmap.xml -o report.html

# Parse XML with Python
python3 -c "import xml.etree.ElementTree as ET; ..."

# Use grep on grepable output for specific ports
grep "22/open" scan.gnmap | awk '{print $2}'
```

### Traceroute
**Definition:** Trace the network path to targets.
```bash
nmap --traceroute 192.168.1.1       # Trace route to target
nmap -A target                       # Includes traceroute in aggressive scan
nmap -sn --traceroute 192.168.1.0/24  # Traceroute without port scan
```

---

## Best Practices

**Definition:** Guidelines for responsible, effective, and professional Nmap usage.

### Legal & Ethical Rules
**Definition:** Always operate within legal and ethical boundaries — violations have serious consequences.
```
✅ DO:
  - Only scan networks you own or have explicit written permission to scan
  - Keep records of authorization (contracts, emails, scope documents)
  - Scan during agreed maintenance windows when possible
  - Report findings responsibly
  - Use the minimum intrusive scan type needed

❌ NEVER:
  - Scan networks you don't own without written permission
  - Use Nmap to facilitate unauthorized access
  - Run DoS-category scripts against production systems
  - Scan cloud providers (AWS, Azure, GCP) without their permission
  - Share scan results of others' systems without authorization
```

### Scan Strategy
**Definition:** Approach scanning methodically to be efficient and avoid disruption.
```bash
# 1. Start with ping scan to find live hosts
nmap -sn 192.168.1.0/24 -oG hosts.gnmap

# 2. Quick scan to find open ports
nmap -p- --min-rate 5000 --open -T4 $(cat hosts.gnmap | grep Up | awk '{print $2}')

# 3. Detailed scan only on open ports
nmap -sV -sC -O -p [open_ports] target

# 4. Targeted vulnerability scanning
nmap --script=vuln -p [relevant_ports] target

# This staged approach:
# - Reduces unnecessary traffic
# - Focuses effort on live hosts
# - Avoids triggering unnecessary alerts
```

### Performance Tuning
**Definition:** Balance speed and accuracy for different scenarios.
```bash
# Internal network — fast
nmap -T4 --min-rate 5000 192.168.1.0/24

# Internet targets — slower, more reliable
nmap -T3 --max-rate 100 target

# Avoid crashing fragile devices (printers, IoT)
nmap -T2 --max-parallelism 1 target

# Large network — parallel but controlled
nmap -T4 --min-hostgroup 64 --min-parallelism 64 192.168.0.0/16
```

### Documentation
**Definition:** Always document your scans properly for professional use.
```bash
# Save all output formats with timestamp
nmap -A -oA "$(date +%Y%m%d_%H%M)_scan_192.168.1.1" 192.168.1.1

# Include scan metadata in filename
nmap -sV -p 80,443 -oA "client_webservers_$(date +%F)" 192.168.1.0/24

# Generate HTML report from XML
xsltproc /usr/share/nmap/nmap.xsl results.xml -o results.html
```

### Summary of Rules

* Always have **written authorization** before scanning any network
* Start with **`-sn` ping scan** to discover live hosts before full scans
* Use **`-T4`** for internal networks, **`-T3`** or slower for internet targets
* Save results with **`-oA`** to get all output formats at once
* Use **`--open`** to show only open ports in results
* Use **`-n`** to skip DNS resolution when speed matters
* Use **`-Pn`** when targets block ping but may have open ports
* Run **`sudo nmap`** — most scan types require root privileges
* Use **specific port lists** instead of scanning all 65535 ports unless necessary
* Document everything — **timestamp**, **scope**, **authorization**, **findings**
