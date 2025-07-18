# 🔍 Scanning Techniques

This section explores various network scanning techniques using `nmap`. Each technique has a unique purpose and level of stealth, speed, and information gathered.

---

## 1️⃣ TCP Connect Scan (`-sT`)

This scan uses a full TCP connection (three-way handshake). It is easily detectable but very reliable.

**Metasploitable Machine**

![TCP Scan](/docs/image/TCP_Scan.png)

```bash
nmap -sT -p1-65535 -v 192.168.1.7
```
`-sT` : TCP connect scan

`-p1-65535/-p-` : Scan all ports

`-v` : Verbose output (Internal details of scans)


⚠️ Detectable by firewalls and IDS due to full handshake.

## 2️⃣ Stealth (Half-Open) Scan (-sS)
Avoids full TCP handshake. Often used to bypass firewalls and avoid detection.

![Stealth Scan](/docs/image/Stealth_Scan.png)

```bash
nmap -sS -p1-65535 -v 192.168.1.1
```
`-sS` : Stealth SYN scan

No complete handshake, avoids basic firewalls

✅ Useful for penetration tests.

## 3️⃣ Version Detection (-sV)
Determines service version running on open ports.
![Version Scan](/docs/image/Version_Scan.png)

```bash
nmap -sV -p- -v 192.168.1.1
```
`-sV` : Service Version detection

`-p-` : All ports

Example: Detects Apache 2.4.29 or OpenSSH 7.6

## 4️⃣ Operating System Detection (-O)
Tries to guess the OS based on TCP/IP fingerprinting.

![OS Scan](/docs/image/OS_Scan.png)

```bash
nmap -sS -O -p- -v 192.168.1.7
```
`-O` : OS detection

**ℹ️ Requires root privileges.**

## 5️⃣ Default Script Scan (-sC)
Runs common NSE (Nmap Scripting Engine) scripts against services.
![Script Scan](/docs/image/Script_Scan.png)
![Script Scan](/docs/image/Script_Scan_1.png)
![Script Scan](/docs/image/Script_Scan_2.png)
```bash
nmap -sC -sV -p- -oX example.xml 192.168.1.7
```
`-sC` : Run default scripts

`-sV` : Service Detection

`-oX` : Save results in XML format

**To convert the XML report to HTML:**

![Xml-Html](/docs/image/XML_to_HTML.png)

- Local hosted html webpage of name example.html with all the details about the ip address.

![XML-Html](/docs/image/Nmap_HTML.png)
```bash
xsltproc example.xml -o example.html
```

## 6️⃣ Aggressive Scan (-A)
Performs OS detection, version detection, script scanning, and traceroute.

![Aggressive Scan](/docs/image/Aggresive_scan.png)
![Aggressive Scan](/docs/image/Aggresive_scan_1.png)
![Aggresive Scan](/docs/image/Aggresive_scan_2.png)
![Aggresive Scan](/docs/image/Aggresive_scan_3.png)
![Aggresive Scan](/docs/image/Aggresive_scan_4.png)
```bash
nmap -A -p- -v 192.168.1.7
```
- Combines multiple scans
- Can be noisy and slow

## 7️⃣ Null Scan (-sN)
Sends packets with no TCP flags set. Useful for firewall evasion.

```bash
nmap -sN -v -p- 192.168.1.7
```
`-sN` : Null Scan

No flags → Stealthy
✔️ No response = Port open
❌ RST = Port closed

## 8️⃣ Fragmentation Scan (-f)
- A fragmented scan in Nmap is used for stealth and evasion — it's a technique to bypass firewalls, intrusion detection systems (IDS), or intrusion prevention systems (IPS) that analyze and block suspicious network traffic.

![Frag](/docs/image/Frag_Scan.png)

![Frag](/docs/image/Frag_Scan_1.png)
```bash
nmap -f -v -p- 192.168.1.7
```
🧩 Obfuscates packet content.

## 9️⃣ Custom MTU Scan (--mtu)
- Sets the Maximum Transmission Unit for probes.
- The `--mtu` option sets a custom packet size (Maximum Transmission Unit).
- It tells Nmap to fragment its packets so each part fits within the MTU size you specify.

**NOTE**
- It prevents Nmap from sending any packet larger than 16 bytes at all.
- So instead of sending one full probe (e.g., 60–100 bytes), Nmap fragments it into tiny pieces, each ≤ 16 bytes.
- **The MTU must be a multiple of 8**


```bash
nmap --mtu=16 -v -p- 192.168.1.7
```
**🔬 Helps evade some firewalls with MTU anomalies.**

## 🔟 Fast Scan (-F)
Scans fewer ports (about 100 well-known ones).

```bash
nmap -F -v -sV 192.168.1.7
```
**⚡ Fast but limited results.**

**🅿️ No Ping Scan (-Pn)**
- Skips host discovery. Useful when ICMP is blocked.

![No Ping](/docs/image/No_Ping_Scan.png)

```bash
nmap -Pn -v -p80 192.168.1.7
```
✅ Ensures scanning even if ICMP echo is filtered.

**🔁 Ping Scan Only (-sn)**
Scans for live hosts in a subnet without port scanning.

![PingScan](/docs/image/Ping_Scan_Only.png)
![PingScan](/docs/image/Ping_Scan_Only_1.png)

```bash
nmap -sn -v 192.168.1.0/24
```
🧭 Good for mapping active hosts.

**✅ TTL-Based OS Detection (via Ping)**
Using ping TTL value to guess OS:
```
TTL (64)   ➜ Likely Linux  
TTL (128)  ➜ Likely Windows  
TTL (254)  ➜ Likely Solaris
```
