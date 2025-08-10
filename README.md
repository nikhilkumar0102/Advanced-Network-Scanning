#  Advanced Network Scanning

A comprehensive guide to advanced network scanning and reconnaissance using tools like **Nmap**, **Netdiscover**, and related utilities. This repository is designed for cybersecurity students, ethical hackers, penetration testers, and network security analysts who want to explore both standard and stealthy scanning methods, service enumeration, firewall evasion, and reporting techniques.

---

##  Table of Contents

- [Introduction](#-introduction)
- [Tools Used](#️-tools-used)
- [Getting Started](#-getting-started)
- [Scanning Techniques](#-scanning-techniques)
- [Firewall Bypass Methods](#-firewall-bypass-methods)
- [Script Usage & Output](#-script-usage--output)
- [Denial of Service Tests](#-denial-of-service-tests)
- [Repository Structure](#-repository-structure)
- [Legal Disclaimer](#️-legal-disclaimer)

---

## Introduction

Network scanning is a fundamental phase of penetration testing and ethical hacking. This project explores:
- Host discovery
- Port scanning
- Service and version enumeration
- OS fingerprinting
- Stealth and obfuscation techniques
- Automation and reporting

---

## Tools Used

| Tool        | Purpose                                 |
|-------------|------------------------------------------|
| `nmap`      | Network mapping, port scanning, OS/service detection |
| `netdiscover` | Passive IP discovery on LAN networks    |
| `xsltproc`  | Transform Nmap XML reports into HTML     |
| `grep`, `ls`, `ping` | Auxiliary tools for discovery and manual filtering |

---

##  Getting Started

To use this repository:

1. **Clone the repo**
   ```bash
   git clone https://github.com/yourusername/Advanced-Network-Scanning.git
   cd Advanced-Network-Scanning

2. **Ensure tools are installed**
   ```bash
   sudo apt install nmap netdiscover xsltproc
   
3. **Run your first scan**
   ```bash
   sudo nmap -sS -p- -v ip_address

## 🔧 Scanning Techniques
The reposity covers:
- TCP Connect `(-sT)`
- Stealth (SYN Scan) `(-sS)`
- Version Detection `(-sV)`
- OS Detection `(-O)`
- Aggressive Scans `(-A)`
- Null `(-sN)`, Xmas `(-sX)`, and Fragmentation scans for stealth `(-f)`
- Fast Scans `(-F)`
- Subnet-wide scans `(-sn)`

Detailed documentation is in:
 [docs/03_Scanning_Techniques.md](docs/03_Scanning_Techniques.md)


##  Firewall Bypass Methods
Learn how to evade detection by:

-   Randomizing hosts `(--randomize-hosts)`
-    Decoy scanning `(-D)`
-    MAC spoofing `(--spoof-mac)`
-    Source port spoofing `(--source-port)`
-    IP spoofing `(-S)`
-    Fragmentation and null scans

See:
 [docs/04_Bypass_Techniques.md](docs/04_Bypass_Techniques.md)

##  Script Usage & Output

- Default and custom Nmap scripts `(.nse)`
- FTP, SMTP enumeration
- NSE script execution for specific ports
- Output in XML `(-oX)` and conversion to HTML using `xsltproc`

See:
 [docs/05_Scripts_and_Examples.md](docs/05_Scripts_and_Examples.md)

**Example**
```bash
   nmap 192.168.1.1 -p- -sC -sV -oX example.xml
   xsltproc example.xml -o example.html
```

##  Denial of Service Tests
Test ICMP-based DoS resistance:
- Packet size manipulation `(ping -s 1000)`
- Preventing fragmentation `(-M do)`
- TTL analysis for OS fingerprinting

See:
 [docs/06_DOS_Attacks.md](docs/06_Dos_and_Attacks.md)

##  Repository Structure

## Repository Structure

```plaintext
Advanced-Network-Scanning/
│
├── README.md
├── docs/
│   ├── 01_Introduction
│   ├── 02_Tools
│   ├── 03_Scanning_Techniques.md
│   ├── 04_Bypass_Techniques.md
│   ├── 05_Scripts_and_Examples.md
│   ├── 06_DOS_Attacks.md
│   └── images/               # Screenshots and diagrams


```
##  Legal Disclaimer

This repository is intended for educational and ethical penetration testing purposes only.  
Unauthorized scanning or attacks on networks you do not own or have explicit permission to test is illegal and unethical.  
Always ensure you have proper authorization before performing any network reconnaissance.

##  **Contributions**  
Contributions are welcome! Feel free to:  
- Add new techniques  
- Improve documentation  
- Include screenshots  
- Suggest best practices


