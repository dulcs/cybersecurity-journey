# 🔍 Nmap Ultimate Cheat Sheet

## 📌 1. Essential & Basic Scans
Ideal for initial target reconnaissance to map out active hosts and open ports.

| Command | Scan Type | Objective / Mechanism |
| :--- | :--- | :--- |
| `nmap <IP>` | **Standard Scan** | Scans the top 1,000 most common ports using a full TCP 3-way handshake. |
| `nmap -sS <IP>` | **SYN Stealth Scan** | Default stealth scan (half-open). Does not complete the TCP connection; evades basic logging. |
| `nmap -sT <IP>` | **TCP Connect Scan** | Completes the TCP connection. Used by default if running without `sudo` privileges. |
| `nmap -sU <IP>` | **UDP Scan** | Scans UDP ports (DNS, DHCP, SNMP). Significantly slower than TCP scanning. |

---

## 🎯 2. Port Selection & Filtering
Narrow down your attack surface to save time and focus on specific active services.

```bash
# Scan a single specific port
nmap -p 80 <IP>

# Scan a list of specific ports (comma-separated)
nmap -p 22,80,443,445 <IP>

# Scan a defined port range
nmap -p 1-1024 <IP>

# THE CTF CLASSIC: Scan all 65,535 possible ports
nmap -p- <IP>

# Fast Mode: Scan only the top 100 most common ports
nmap -F <IP>
````

## 🧠 3. Service, OS, and Script Detection

The key to finding vulnerabilities. This determines the exact software version running behind an open port.

- **`-sV` (Version Detection):** Interrogates open ports to determine the exact service name and software version.
    
- **`-sC` (Default Scripts):** Runs safe, non-intrusive scripts from the Nmap Scripting Engine (NSE) to check for common misconfigurations or default credentials.
    
- **`-O` (OS Detection):** Analyzes the TCP/IP fingerprint response to deduce the target operating system (Linux, Windows, etc.).
    

> 🔥 **The Infrastructure Golden Combo:**
> 
> Bash
> 
> ```
> nmap -sC -sV -O -p- <IP>
> ```
> 
> _Run this comprehensive command once you have identified which ports are open to gather deep technical intelligence all at once._

## ⚡ 4. Timing & Performance (Timing Templates)

Controls the speed and aggressiveness of the scan. Essential for balancing network stability against CTF time constraints.

Use the `-T<0-5>` flag to set the template:

- **`-T0` (Paranoid) / `-T1` (Sneaky):** Ultra-slow scans designed to bypass Intrusion Detection Systems (IDS).
    
- **`-T3` (Normal):** The default Nmap speed setting.
    
- **`-T4` (Aggressive):** **The recommended setting for CTFs and lab environments.** Speeds up probes assuming a reliable, fast network connection.
    
- **`-T5` (Insane):** Extreme speed. Highly likely to drop packets or crash fragile legacy services if the network is unstable.
    

Bash

```
# Aggressive, fast-paced scan for time-restricted environments
nmap -p- -T4 <IP>
```

## 🤖 5. Nmap Scripting Engine (NSE)

Automates vulnerability scanning using Nmap's built-in script database.

Bash

```
# Run a specific script (e.g., check for the SMB EternalBlue vulnerability)
nmap -p 445 --script smb-vuln-ms17-010 <IP>

# Run an entire category of scripts (e.g., vuln, auth, discovery)
nmap -p 80 --script vuln <IP>

# Brute-force discover hidden directories on a target web server
nmap -p 80 --script http-enum <IP>
```

## 💾 6. Output Formats

Save your terminal results directly to your workspace so you never lose your evidence.

- **`-oN` (Normal Output):** Saves the scan results exactly as they appear on your terminal screen.
    
- **`-oX` (XML Output):** Structured format used for importing data into third-party tools like Zenmap or Metasploit.
    
- **`-oG` (Grepable Output):** Clean, single-line format ideal for extracting active ports using commands like `grep`, `awk`, or `cut`.
    
- **`-oA` (Output All Formats):** **Highly Recommended.** Saves the results in all three formats simultaneously under the specified base filename.
    

Bash

```
# Run a thorough scan and log all formats for your report directory
nmap -sC -sV -p- -oA thm-recon-target <IP>
```