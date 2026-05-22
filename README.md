# 🔐 TLS Security Analysis — Vulnerable TLS Infrastructure (Person 2)

## 📌 Objective

This module is responsible for building intentionally vulnerable HTTPS localhost servers for demonstrating RSA cryptographic attacks in TLS environments.

The infrastructure is used for:
- TLS handshake analysis
- Public key extraction
- RSA attack demonstrations
- Weak certificate detection
- Wireshark packet capture

---

# 👨‍💻 Person 2 Responsibilities

Person 2 is responsible for:

✅ Vulnerable RSA key generation  
✅ TLS certificate creation  
✅ HTTPS localhost servers  
✅ Wireshark TLS capture  
✅ Public key extraction  

Person 2 does **NOT**:
- perform cryptographic attacks
- recover private keys
- implement RSA attacks
- create Java analyzer

---

# 🛠️ Software Requirements

## Install Required Software

### Python
Install Python 3.11+

### OpenSSL
Used for:
- RSA certificate generation
- TLS key inspection
- Public key extraction

### Wireshark
Used for:
- TLS handshake capture
- Certificate packet analysis

---

# 📦 Python Dependencies

Install required libraries:

```bash
pip install pycryptodome sympy
```

---

# 📁 Project Structure

```text
tls_project/
│
├── fermat_server/
│
├── wiener_server/
│
├── gcd_server/
│
└── screenshots/
```

---

# 1️⃣ Fermat Vulnerable TLS Server

## 📌 Vulnerability

The RSA primes are intentionally generated close together.

This makes the modulus vulnerable to Fermat factorization.

---

## 📁 Files

```text
fermat_server/
│
├── generate_fermat.py
├── fermat.pem
├── fermat.crt
├── server.py
└── index.html
```

---

## 🔑 Generate Vulnerable RSA Key

Run:

```bash
python generate_fermat.py
```

Output:

```text
fermat.pem
```

---

## 📜 Generate TLS Certificate

Run:

```bash
openssl req -new -x509 -key fermat.pem -out fermat.crt -days 365
```

Important:

```text
Common Name = localhost
```

---

## 🌐 Run HTTPS Server

Run:

```bash
python server.py
```

Server URL:

```text
https://localhost:4443
```

---

# 2️⃣ Wiener Vulnerable TLS Server

## 📌 Vulnerability

Uses intentionally weak RSA configuration suitable for Wiener attack demonstrations.

---

## 📁 Files

```text
wiener_server/
│
├── generate_wiener.py
├── wiener.pem
├── wiener.crt
├── server.py
└── index.html
```

---

## 🔑 Generate RSA Key

Run:

```bash
python generate_wiener.py
```

---

## 📜 Generate TLS Certificate

Run:

```bash
openssl req -new -x509 -key wiener.pem -out wiener.crt -days 365
```

---

## 🌐 Run HTTPS Server

Run:

```bash
python server.py
```

Server URL:

```text
https://localhost:4444
```

---

# 3️⃣ Batch GCD Vulnerable TLS Servers

## 📌 Vulnerability

Two RSA keys intentionally share a common prime.

This makes both keys vulnerable to Batch GCD attacks.

---

## 📁 Files

```text
gcd_server/
│
├── generate_gcd.py
├── gcd1.pem
├── gcd2.pem
├── gcd1.crt
├── gcd2.crt
├── gcd_server1.py
├── gcd_server2.py
└── index.html
```

---

## 🔑 Generate Shared Prime Keys

Run:

```bash
python generate_gcd.py
```

Outputs:
- gcd1.pem
- gcd2.pem

---

## 📜 Generate TLS Certificates

Run:

```bash
openssl req -new -x509 -key gcd1.pem -out gcd1.crt -days 365
```

Run:

```bash
openssl req -new -x509 -key gcd2.pem -out gcd2.crt -days 365
```

---

## 🌐 Run HTTPS Servers

### Terminal 1

```bash
python gcd_server1.py
```

### Terminal 2

```bash
python gcd_server2.py
```

Server URLs:

```text
https://localhost:4445
https://localhost:4446
```

---

# 📡 TLS Handshake Analysis

## Open Wireshark

Select:

```text
Adapter for loopback traffic capture
```

---

## Apply TLS Filter

```text
tls
```

---

## Capture Required Packets

Capture:
- ClientHello
- ServerHello
- Certificate

---

# 🔍 Public Key Extraction

For each server run:

```bash
openssl rsa -in <key>.pem -text -noout
```

Extract:
- modulus (n)
- exponent (e)

These values are provided to the attack implementation team.

---

# ⚠️ Expected Browser Behavior

Each localhost server will display:

```text
Your connection is not private
```

This is expected because:
- self-signed certificates are used
- weak TLS configurations are intentional

---

# 🌐 Final Running Servers

| Server | Port | Vulnerability |
|--------|------|----------------|
| Fermat Server | 4443 | Close RSA primes |
| Wiener Server | 4444 | Weak RSA configuration |
| GCD Server 1 | 4445 | Shared prime |
| GCD Server 2 | 4446 | Shared prime |

---

# 📷 Required Screenshots

Capture screenshots of:
- Browser TLS warnings
- ClientHello packet
- ServerHello packet
- Certificate packet
- TLS handshake capture
- Running localhost servers
  
---

# 📌 Notes

These vulnerable TLS systems are intentionally designed ONLY for:
- localhost testing
- academic research
- cryptographic demonstrations
- controlled security analysis

No attacks are performed against external systems.
