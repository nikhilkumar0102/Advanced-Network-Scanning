# ⚙️ Scripts and Examples

This section provides real-world examples of using **custom scripts** and **built-in Nmap NSE (Nmap Scripting Engine) scripts** to gather in-depth information about target services.

---

## 📁 Where are Nmap scripts stored?

Default Nmap NSE scripts are located in:

```bash
/usr/share/nmap/scripts/
These files use the .nse extension.
```
You can list available scripts with:

bash
Copy code
ls /usr/share/nmap/scripts/
To search for a specific protocol-related script:

bash
Copy code
ls /usr/share/nmap/scripts/ | grep "ftp"
🔍 Example: FTP Script Scan
Scan for all FTP-related vulnerabilities or banners:

bash
Copy code
nmap -p21 --script=ftp* 192.168.1.1
This will use scripts like:

ftp-anon.nse – checks for anonymous login

ftp-bounce.nse – tests for FTP bounce attack vulnerability

ftp-vsftpd-backdoor.nse – checks for vsFTPd backdoor

📩 SMTP Script Example
Scan for email-related services on port 25:

bash
Copy code
nmap -p25 --script=smtp* 192.168.1.1
This can help detect:

Open relays

SMTP user enumeration

Service banners

🧪 Manually Selecting Scripts
Use exact script name or wildcards:

bash
Copy code
nmap -p80 --script=http-title 192.168.1.1
nmap -p80 --script=http* 192.168.1.1
📜 Writing a Custom NSE Script
NSE scripts are written in Lua. You can create your own custom logic for service testing.

Example: Custom Hello World script
lua
Copy code
description = [[
Prints Hello World on every scan.
]]

author = "Nikhil Kumar"

categories = {"default"}

action = function()
  return "Hello from NSE script!"
end
Save this as hello.nse and run it like:

bash
Copy code
nmap --script ./hello.nse 127.0.0.1
🧰 Useful NSE Script Categories
Category	Description
auth	Authentication bypass or brute force
broadcast	Broadcast discovery
default	Scripts run with -sC
dos	Denial of Service test scripts
exploit	Known exploit attempts
vuln	Common vulnerability checks
safe	Non-intrusive scans

🎯 Tip: Use Verbose Mode
Always combine scripts with -v or -vv to see detailed script output:

bash
Copy code
nmap -p80 --script=http-title -v 192.168.1.1
💡 Combining with Port and Version Scan
bash
Copy code
nmap -sS -sV -p21,22,80,139,445 --script=default,vuln 192.168.1.1
This will:

Stealth scan selected ports

Detect service versions

Run common and vulnerability scripts

✅ Summary
Use --script=<name> to run scripts.

Use wildcards (ftp*, http*) to run multiple scripts by topic.

Explore /usr/share/nmap/scripts/ for ideas.

NSE scripts can automate detection of many known vulnerabilities and misconfigurations.

🔒 Always use scripts ethically and only on machines you own or are authorized to test.
