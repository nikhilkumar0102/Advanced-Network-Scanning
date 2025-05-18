# 🔐 Firewall Bypass Techniques

In secured environments, firewalls and Intrusion Detection Systems (IDS/IPS) may block or detect basic scans. This section outlines **Nmap techniques** to **evade detection**, **bypass filters**, and **scan stealthily**.

> ⚠️ Use these techniques only in **authorized** environments like penetration testing labs or CTFs.

---

## 🎄 1. Xmas Scan (`-sX`)

Xmas scans set **FIN, URG, and PUSH** TCP flags in packets — resembling a "blinking Christmas tree".

![XmasScan](/docs/image/Xmas_scan.png)
```bash
nmap -sX -v 192.168.1.7
```
Works well against systems using RFC-compliant TCP stack.

- Behavior:
   - No response = port open
   - RST response = port closed

❌ Doesn't work on Windows machines (non-RFC compliant TCP stack).

## 🎲 2. Decoy Scan (`-D`)
Generates fake IP addresses as decoys to hide the real source IP of the scanner.

![Decoy](/docs/image/Decoy.png)
```bash
nmap -D RND:10 -v 192.168.1.7
```
- `RND:10` : Nmap will use 10 random IPs as decoys.
- Real IP gets `"lost"` among decoys.
- Useful to evade logging and attribution.

## 🔀 3. Randomize Host Order (`--randomize-hosts`)
Randomizes the order of IP addresses scanned to confuse detection systems.

```bash
nmap 192.168.1.0/24 -p- -v --randomize-hosts
```
**🧠 Prevents predictable scanning patterns.**

## 🧅 4. IP Spoofing (`-S`)
Spoofs source IP (requires privileged access and routing capability).

```bash
nmap -S 192.168.5.10 192.168.1.7
```
`-S` : Source IP to spoof

Only works if the spoofed IP can receive replies (i.e., sniff traffic)
**⚠️ Requires access to spoofed network path (advanced).**

## 🧑‍💻 5. MAC Spoofing (`--spoof-mac`)
Fakes the MAC address sent with packets. Helpful to impersonate known/trusted devices.

```bash
nmap --spoof-mac apple 192.168.1.7
```
- Common vendor names: `apple`, `nokia`, `microsoft`
- Can also use full `MAC-address`

🔧 May bypass MAC-based firewall rules or profiling.

## 🛡️ 6. No Ping (`-Pn`)
Skips host discovery phase (ICMP echo), useful if ICMP is blocked.

```bash
nmap -Pn -v -p80 192.168.1.7
```
- Useful when firewall drops ping/echo requests
- Forces Nmap to assume host is up

## 🎯 7. Source Port Spoofing (`--source-port`)
- Spoofs the source port of packets to appear as a trusted service (e.g., DNS or HTTP).

```bash
nmap --source-port 53 -Pn -v 192.168.1.7
```
- Port 53 mimics DNS traffic
- May bypass port-based filtering

🧪 Some firewalls allow traffic from known service ports.

## 🔕 8. Null Scan (`-sN`)
- Sends packets with no TCP flags set.

```bash
nmap -sN -v -p- 192.168.1.7
```
- Stealthy scan
- Useful to bypass older firewalls/IDS
- Behavior:
- - No response = port open
- - RST = port closed

**📌 Only works on UNIX-like targets.**

## 🧩 9. Packet Fragmentation (`-f`)
- Splits packets into smaller fragments to evade deep packet inspection (DPI).

```bash
nmap -f -v -p- 192.168.1.7
```
Makes it harder for firewalls to reconstruct full packets and inspect them.

## ⚙️ 10. Custom MTU (`--mtu`)
Sets the Maximum Transmission Unit (MTU) for packet fragmentation.

```bash
nmap --mtu=15 -v -p- 192.168.1.7
```
Helps in obfuscation; must use multiples of 8.

## 📊 Summary Table

| Technique           | Flag/Command             | Purpose                            | Notes                              |
|---------------------|--------------------------|-------------------------------------|-------------------------------------|
| Xmas Scan           | `-sX`                    | Stealthy scan via TCP flag abuse    | Not effective on Windows            |
| Decoy Scan          | `-D RND:10`              | Hide origin IP                      | IDS logs are spoofed                |
| Random Hosts        | `--randomize-hosts`      | Avoid detection by order            | Use in subnet scans                 |
| IP Spoofing         | `-S <fake_ip>`           | Hide identity completely            | Advanced setup required             |
| MAC Spoofing        | `--spoof-mac <vendor>`   | Bypass MAC-based rules              | Use known/trusted vendors           |
| No Ping             | `-Pn`                    | Skip ICMP phase                     | Treats all targets as "up"          |
| Source Port Spoof   | `--source-port <port>`   | Evade port-based filtering          | Port 53 (DNS) often allowed         |
| Null Scan           | `-sN`                    | Send packets with no flags          | Stealthy against some firewalls     |
| Fragmentation       | `-f`                     | Split packets                       | Helps avoid DPI detection           |
| Custom MTU          | `--mtu=15`               | Set packet size manually            | Works with multiples of 8           |



✅ Combine techniques like `-sS` `-Pn` `--spoof-mac` for layered stealth in advanced testing scenarios.
