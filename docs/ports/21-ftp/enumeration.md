# FTP Enumeration & Exploitation (Metasploitable 2)

> **Lab Environment:** Metasploitable 2 (Authorized Lab)
>
> **Target IP:** `192.168.56.108`

---

# Objective

Identify the FTP service running on the target, enumerate its version, research known vulnerabilities, and verify whether the service is vulnerable in a controlled lab environment.

---

# Step 1 - Initial Enumeration

Perform a basic Nmap scan to discover open ports.

```bash
nmap 192.168.56.108
```

Example output:

```
21/tcp   open   ftp
22/tcp   open   ssh
23/tcp   open   telnet
80/tcp   open   http
139/tcp  open   netbios-ssn
445/tcp  open   microsoft-ds
3306/tcp open   mysql
...
```

The scan revealed that **FTP (Port 21)** is open.

---

# Step 2 - FTP Service Enumeration

Perform version detection.

```bash
nmap -p 21 -sV -O 192.168.56.108
```

Example:

```
PORT   STATE SERVICE VERSION
21/tcp open  ftp     vsftpd 2.3.4
```

The scan also provides operating system detection.

---

# Step 3 - Vulnerability Research

After identifying the FTP version:

```
vsftpd 2.3.4
```

Search public vulnerability databases such as:

- Rapid7
- CVE Database
- Exploit Database
- NVD

Research indicates that **vsftpd 2.3.4** contains a well-known backdoor vulnerability in the intentionally vulnerable version included with Metasploitable 2.

---
