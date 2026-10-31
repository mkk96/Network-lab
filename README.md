# Network Lab

> Computer networks and cryptography lab programs: classical ciphers, RSA, Diffie-Hellman and socket-based client/server apps in Python and Java.

![Python](https://img.shields.io/badge/Python-3-3776AB?style=flat-square&logo=python&logoColor=white)
![Java](https://img.shields.io/badge/Java-ED8B00?style=flat-square&logo=openjdk&logoColor=white)
![Sockets](https://img.shields.io/badge/TCP-sockets-555555?style=flat-square)
![MySQL](https://img.shields.io/badge/MySQL-4479A1?style=flat-square&logo=mysql&logoColor=white)

## Overview

This repository collects the programs from the Computer Networks lab during my B.Tech in Computer Science at Jamia Millia Islamia (uploaded in December 2017). It covers two areas:

- **Cryptography.** Classical and public-key ciphers. Most have a standalone `cipherDemo.py` that encrypts and decrypts text typed in by the user, plus a `client.py` / `server.py` pair that sends the ciphertext over a TCP socket and decrypts it on the server.
- **Socket programming.** Multi-threaded chat applications, a remote database client/server backed by MySQL, and an SMTP-style mail client/server in Java.

Each cipher folder also has a `ReadMe.md` that explains the algorithm with worked examples.

> **Credits:** this was shared lab material. The cipher demos (`01`–`06`) carry an author credit for Shivanshu Chaudhary ("MohMaya") in their headers, and the cipher notes link to images in his [CollegeCodes](https://github.com/MohMaya/CollegeCodes) repository. This repository is a copy of the lab collection, not entirely original work.

## Programs

### Cryptography

| # | Program | What it does | Files |
| --- | --- | --- | --- |
| 01 | [Substitution Cipher](01%20Substitution%20Cipher/) | Caesar-style shift cipher (each character shifted by 13 in the 0–255 range) | `cipherDemo.py` (the client/server files are empty) |
| 02 | [Transposition Cipher](02%20Transposition%20Cipher/) | Rail Fence cipher with 3 rails; the client encrypts and the server decrypts | `cipherDemo.py`, `client.py`, `server.py` |
| 03 | [Playfair Cipher](03%20Play%20Fair%20Cipher/) | Digraph substitution using a 5×5 key square | `cipherDemo.py`, `client.py`, `server.py` |
| 04 | [Hill Cipher](04%20Hill%20Cipher/) | Polygraphic cipher with a 3×3 key matrix mod 26; decryption uses the modular inverse (adjugate and determinant) | `cipherDemo.py`, `client.py`, `server.py` |
| 05 | [RSA Encryption](05%20RSA%20Encryption/) | Key generation from two user-supplied primes, then encryption and decryption of a numeric message | `cipherDemo.py`, `client.py`, `server.py` |
| 06 | [Vernam Cipher](06%20Vernam%20Cipher/) | One-time-pad style cipher: each character is combined with a key of the same length (mod 128) | `cipherDemo.py`, `client.py`, `server.py` |
| 07 | [Diffie-Hellman Key Exchange](07%20Diffie-Hellman%20Algorithm/) | Two peers choose a prime *p* and primitive root *g*, exchange public values over TCP and confirm that they derived the same shared key | `sideA.py`, `sideB.py` |
| 08 | [64-bit DES](08%2064%20bit%20DES/) | Simplified DES-style Feistel network: 16 rounds with expansion, S-box substitution and hard-coded round keys. It encrypts a fixed 64-bit block and decrypts it again. It uses a single S-box and skips the initial and final permutations. | `cipherDemo.py` |

### Socket programming

| # | Program | What it does | Files |
| --- | --- | --- | --- |
| 26 | [Multi-Way Chat](26%20Multi%20Way%20Chat/) | Full-duplex chat between one server and one client, with separate sender and receiver threads | `server.py`, `client.py`, `threadDemo.py` (threading and queue experiments) |
| 27 | [Remote Database](27%20Remote%20Database/) | Menu-driven client that builds SQL (create table, insert, conditional select, aggregates, delete) and sends it to a multi-threaded server, which runs it on MySQL through PyMySQL | `server.py`, `client.py`, plus prototypes `demo.py`, `menuDemo.py`, `parseDemo.py` |
| 28 | [Many-to-Many Chat](28%20Many%20To%20Many%20Chat/) | Group chat: the server accepts many clients and broadcasts every message to all of them | `server.py`, `client.py`, `threadDemo.py` |
| – | [Database (Java)](Database/) | Multi-threaded TCP server (port 8085) over MySQL/JDBC; the client offers insert, select by ID or column, select all, update and delete | `server.java`, `client.java` |
| – | [Mail (Java)](Smtp/) | SMTP-style mail system: users log in, send mail to other users and list or read their inbox and sent items (mailboxes are kept in memory on the server) | `server.java`, `client.java` |

Folders `09`–`25` (Hamming code, TCP/UDP basics, routing algorithms, Stop-and-Wait, Sliding Window, MD5, SHA-1, AES and others) are placeholders. They contain only an empty `ReadMe.md` and no code yet.

## How to run

**Requirements:** Python 3. Only the standard library is needed (`socket`, `threading`, `queue`), except for `27 Remote Database`, which needs `pip install pymysql` and a running MySQL server.

**Standalone cipher demos**

```bash
cd "03 Play Fair Cipher"
python3 cipherDemo.py
```

**Client/server programs.** Both sides connect to `socket.gethostname()` on port `8080`, so run them in two terminals on the same machine and start the server first:

```bash
# terminal 1
cd "02 Transposition Cipher"
python3 server.py

# terminal 2
cd "02 Transposition Cipher"
python3 client.py
```

For Diffie-Hellman, `sideB.py` is the listening side, so start it first and then run `sideA.py`.

**Remote Database (Python).** Before starting, edit the `pymysql.connect(...)` settings in `server.py` (host, user, password, database, port) to match your local MySQL instance.

**Java programs.** Each file declares a public class whose name differs from the file name, so rename the files before compiling: in `Database/`, rename `server.java` to `Server.java` and `client.java` to `Client.java`; in `Smtp/`, rename them to `MailClientServer.java` and `MailClient_Client.java`. The database server also needs the MySQL Connector/J driver on the classpath and the JDBC URL and credentials in `Server.java` updated for your setup.

```bash
cd Smtp
javac MailClientServer.java MailClient_Client.java
java MailClientServer      # terminal 1
java MailClient_Client     # terminal 2
```

---

Made by [Mukul Kumar](https://mkk96.github.io) · [GitHub](https://github.com/mkk96) · [LinkedIn](https://www.linkedin.com/in/mukul-kumar-60322616b/)
