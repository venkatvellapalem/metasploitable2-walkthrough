# DNS Enumeration

## Service Detection

```bash
nmap -sV -p 53 10.0.2.4
```

### Result

- Port `53/tcp` is open.
- DNS Server: **ISC BIND 9.4.2**

---
<img width="815" height="207" alt="image" src="https://github.com/user-attachments/assets/2f3baadf-62b0-4fab-85cf-937fb7a617d4" />

## Default NSE Scan

```bash
nmap -sC -p 53 10.0.2.4
```

### Result

- Detected DNS service using the `dns-nsid` script.
- Server version identified as **BIND 9.4.2**.

---
<img width="722" height="232" alt="image" src="https://github.com/user-attachments/assets/75bfc4d8-3bee-42a5-ac7d-de96d738886f" />

## DNS NSE Enumeration

```bash
nmap --script dns-* -p 53 10.0.2.4
```

### Result

- DNS server detected.
- Version: **BIND 9.4.2**
- Zone transfer could not be tested because no domain name was provided.
- DNS brute-force and enumeration scripts could not determine a valid domain.

  <img width="912" height="410" alt="image" src="https://github.com/user-attachments/assets/993b541c-9328-4a57-a46d-1fea52155d5c" />


---

## Zone Transfer Attempt

```bash
dig axfr @10.0.2.4
```

### Result

- Zone transfer was unsuccessful.
- No DNS zone information was disclosed.


<img width="515" height="560" alt="image" src="https://github.com/user-attachments/assets/acc077c1-9a24-4474-9c57-373afd26bd08" />

---

## Findings

- DNS service is running on **Port 53**.
- Server software identified as **ISC BIND 9.4.2**.
- No successful zone transfer.
- No domain information could be enumerated.
