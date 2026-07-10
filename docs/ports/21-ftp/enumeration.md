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

<img width="850" height="672" alt="Screenshot 2026-07-10 123829" src="https://github.com/user-attachments/assets/609a15ef-cd03-4bbf-99f5-7458d74e6a2f" />

The scan revealed that **FTP (Port 21)** is open.

---

# Step 2 - FTP Service Enumeration

Perform version detection.

```bash
nmap -p 21 -sV -O 192.168.56.108
```

Example:

<img width="1092" height="397" alt="Screenshot 2026-07-10 123904" src="https://github.com/user-attachments/assets/8e77ded4-0b85-4588-a0f5-c97a63302206" />

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

<img width="1477" height="770" alt="Screenshot 2026-07-10 123954" src="https://github.com/user-attachments/assets/c9ff4b44-fa33-49a4-a96d-6f9586580469" />

Research indicates that **vsftpd 2.3.4** contains a well-known backdoor vulnerability in the intentionally vulnerable version included with Metasploitable 2.

---
