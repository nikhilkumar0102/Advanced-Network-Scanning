# 🧠 Scripts and Examples

This section includes manual and automated scanning examples using **Nmap Scripting Engine (NSE)** and custom shell commands. NSE scripts can enhance scans by detecting vulnerabilities, brute-forcing credentials, and extracting sensitive service data.

---

## 📂 NSE Script Basics

Nmap scripts are located in:

```bash
/usr/share/nmap/scripts/
```
![ScriptList](/docs/image/Scripts.png)
**All scripts end with `.nse`.**

## 📜 Running All Default Scripts
```bash
nmap -sC -sV -v 192.168.1.7
```
`-sC` : Run default scripts

`-sV` : Service version detection

## ⚙️ Manual NSE Script Examples
**1️⃣ FTP Vulnerability Scan**

![FTPScript](/docs/image/Scripts_3FTP.png)
![FTPScript](/docs/image/Scripts_4FTP.png)
```bash
nmap -p21 --script=ftp* -v 192.168.1.7
```
- Scans FTP-related vulnerabilities and configurations

**Example scripts:**
![FTP](/docs/image/Scripts_1.png)


- `ftp-anon.nse` : Check for anonymous login

- `ftp-vsftpd-backdoor.nse`: Detect backdoored vsftpd versions

**2️⃣ SSH Scan**
```bash
nmap -p22 --script=ssh* -v 192.168.1.7
```
- `ssh-hostkey.nse` : Extracts the SSH host key

- `ssh-auth-methods.nse` : Lists supported auth methods

**3️⃣ HTTP Enumeration**
```bash
nmap -p80,443 --script=http* -v 192.168.1.7
```
Examples:

- `http-title.nse` : Extracts page title

- `http-enum.nse` : Lists common paths (like /admin)

- `http-vuln* `: Checks for known web vulnerabilities

**🔐 SMTP Scan Example**
Find SMTP Services

```bash
ls | grep smtp
```
Script-Based Scan
```bash
nmap -p25 --script=smtp* -v 192.168.1.7
```
  -  `smtp-open-relay.nse` : Checks if the server is open relay

  -  `smtp-commands.nse` : Retrieves supported SMTP commands

**📄 Output Report Automation**
Save XML Report
```bash
nmap -sC -sV -p- -oX reports/example.xml 192.168.1.7
```
- Convert XML to HTML
```bash
xsltproc reports/example.xml -o reports/example.html
```
- This provides a beautiful, browsable report file for documentation or presentations.

🧰 Script Discovery & Usage Tips
Search scripts by keyword:
```bash
ls /usr/share/nmap/scripts | grep ssh
```
Check script arguments:

```bash
nmap --script-help=ftp-anon
```

## ✅ Summary of Useful NSE Scripts

| Service | NSE Script                   | Description                     |
|---------|------------------------------|---------------------------------|
| FTP     | `ftp-anon.nse`              | Checks for anonymous login      |
| FTP     | `ftp-vsftpd-backdoor.nse`   | Detects backdoor vulnerability  |
| SSH     | `ssh-hostkey.nse`           | Extracts SSH key                |
| SSH     | `ssh-auth-methods.nse`      | Lists allowed auth methods      |
| HTTP    | `http-title.nse`            | Grabs HTML title                |
| HTTP    | `http-enum.nse`             | Brute-force path discovery      |
| SMTP    | `smtp-open-relay.nse`       | Detects open relay issues       |


📌 Notes
- Always run Nmap with `root privileges` for full functionality.

- Some NSE scripts may take time or trigger alerts on target IDS/IPS.

- Combine with firewalls bypass (`-Pn`, `-f`, `--mtu`, etc.) when needed.
