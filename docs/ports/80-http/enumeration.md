# Enumeration Report

## Target Information

| Item | Value |
|------|-------|
| Target IP | 10.0.2.4 |
| Scanner | Nmap 7.99 |
| Scan Type | TCP Connect Scan |
| Date | 10 July 2026 |

---

# Nmap Scan

Command Used

```bash
nmap 10.0.2.4
```

---

## Scan Results

```
21/tcp   open  ftp
22/tcp   open  ssh
23/tcp   open  telnet
25/tcp   open  smtp
53/tcp   open  domain
80/tcp   open  http
111/tcp  open  rpcbind
139/tcp  open  netbios-ssn
445/tcp  open  microsoft-ds
512/tcp  open  exec
513/tcp  open  login
514/tcp  open  shell
1099/tcp open  rmiregistry
1524/tcp open  ingreslock
2049/tcp open  nfs
2121/tcp open  ccproxy-ftp
3306/tcp open  mysql
5432/tcp open  postgresql
5900/tcp open  vnc
6000/tcp open  X11
6667/tcp open  irc
8009/tcp open  ajp13
8180/tcp open  unknown
```

---

# Open Services Analysis

## FTP (21)

Purpose

- File Transfer Protocol
- Used for uploading/downloading files.

Possible Checks

- Anonymous login
- Weak credentials
- Writable directories

Commands

```bash
ftp 10.0.2.4
```

---

## SSH (22)

Purpose

Secure remote login.

Checks

- Weak passwords
- SSH version
- Supported algorithms

Command

```bash
ssh user@10.0.2.4
```

---

## Telnet (23)

Purpose

Remote administration.

Observation

Telnet sends credentials in plaintext.

Risk

High

Commands

```bash
telnet 10.0.2.4
```

---

## SMTP (25)

Purpose

Mail Server

Checks

- User Enumeration
- Open Relay

Example

```bash
nc 10.0.2.4 25
```

---

## DNS (53)

Purpose

Domain Name Service

Checks

- Zone Transfer
- Version Detection

Commands

```bash
dig axfr @10.0.2.4
```

---

## HTTP (80)

Purpose

Web Server

Checks

- Hidden directories
- Web technologies
- Login pages

Tools

- Gobuster
- Nikto
- WhatWeb

Commands

```bash
whatweb http://10.0.2.4

nikto -h http://10.0.2.4

gobuster dir -u http://10.0.2.4 -w /usr/share/wordlists/dirb/common.txt
```

---

## RPCBind (111)

Purpose

Maps RPC services.

Checks

```bash
rpcinfo -p 10.0.2.4
```

---

## SMB (139,445)

Purpose

Windows File Sharing

Checks

- Null Sessions
- Shared folders
- SMB Version

Commands

```bash
smbclient -L //10.0.2.4/

enum4linux 10.0.2.4
```

---

## R Services (512,513,514)

Services

- rexec
- rlogin
- rsh

Observation

These are legacy remote administration services.

Risk

Very High

---

## Java RMI (1099)

Purpose

Java Remote Method Invocation

Check

```bash
nmap --script rmi-dumpregistry -p1099 10.0.2.4
```

---

## NFS (2049)

Purpose

Network File System

Commands

```bash
showmount -e 10.0.2.4
```

---

## FTP Alternate (2121)

Purpose

Alternative FTP Service

Checks

- Anonymous login
- Weak authentication

---

## MySQL (3306)

Purpose

Database Server

Checks

- Default credentials
- Database enumeration

Commands

```bash
mysql -h 10.0.2.4 -u root -p
```

---

## PostgreSQL (5432)

Purpose

Database Server

Commands

```bash
psql -h 10.0.2.4 -U postgres
```

---

## VNC (5900)

Purpose

Remote Desktop

Checks

Password authentication

---

## X11 (6000)

Purpose

Linux Graphical Server

Observation

Can sometimes allow remote display connections.

---

## IRC (6667)

Purpose

Internet Relay Chat

Checks

Service banner

---

## AJP13 (8009)

Purpose

Apache JServ Protocol

Possible Risk

Ghostcat (CVE-2020-1938)

Commands

```bash
nmap -sV -p8009 10.0.2.4
```

---

## Port 8180

Purpose

Unknown

Next Step

Identify service

```bash
nmap -sV -p8180 10.0.2.4
```

---

# Initial Findings

Large attack surface observed.

Several legacy protocols are enabled:

- FTP
- Telnet
- Rlogin
- RSH
- Rexec

Database services exposed:

- MySQL
- PostgreSQL

Remote administration services exposed:

- SSH
- VNC

Web services available:

- HTTP
- AJP

File sharing services:

- SMB
- NFS

---

# Next Enumeration Steps

- Perform Service Version Detection

```bash
nmap -sV -A 10.0.2.4
```

- Detect Operating System

```bash
nmap -O 10.0.2.4
```

- Run NSE Scripts

```bash
nmap --script vuln 10.0.2.4
```

- Enumerate SMB

```bash
enum4linux 10.0.2.4
```

- Scan Web Server

```bash
nikto -h http://10.0.2.4
```

- Directory Brute Force

```bash
gobuster dir -u http://10.0.2.4 -w /usr/share/wordlists/dirb/common.txt
```

---

# Conclusion

The target exposes numerous services, including several legacy and potentially insecure protocols. Further enumeration is required to identify service versions, misconfigurations, weak credentials, and known vulnerabilities before proceeding to exploitation.
<img width="641" height="547" alt="Screenshot 2026-07-10 142214" src="https://github.com/user-attachments/assets/1999d765-fbc2-43a9-b482-4b3156adebb9" />
