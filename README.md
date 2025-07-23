#  Distributed File Orchestration and Synchronization (DFOS)

A multi-client authenticated file transfer system in Python using socket programming. The server handles multiple clients concurrently, each with isolated file operations.

---

##  High-Level Design (HLD)

```
                         +-----------------------------+
                         |         Client CLI          |
                         |-----------------------------|
                         | - Authenticate via CLI      |
                         | - Upload / Download Files   |
                         | - Delete / Preview Files    |
                         | - List Own Files            |
                         +-----------------------------+
                                   |
                          [ TCP Socket Communication ]
                                   |
+-------------------------------+       Multi-threaded       +-------------------------------+
|          Client #1            | <-------------------------> |                               |
|          Client #2            | <-------------------------> |           Server              |
|          ...                  | <-------------------------> | (ThreadPoolExecutor - max 10) |
+-------------------------------+                             +-------------------------------+
                                                                | - Authenticates users
                                                                | - Handles file actions
                                                                | - Spawns thread per client
                                                                | - Logs events and performance
                                                                | - Gracefully shuts down
                                                                +-----------------------------+
```

---

##  Project Structure

```
DFOS/
├── server.py               # Server handling concurrent clients via threads
├── client.py               # CLI interface for user operations
├── id_passwd.txt           # Stored credentials for login
├── server_storage/         # Per-user folders to isolate files
├── server_performance.log  # CPU/memory logs and server performance
└── README.md
```

---

##  Features

-  User Authentication (via `id_passwd.txt`)
-  Upload File
-  Download File
-  Preview File (first 1024 bytes)
-  List Own Files
-  Delete File
-  Server logs performance: CPU, memory usage
-  Graceful Shutdown (interrupt-safe)
-  Multi-threaded: Handles up to 10 clients concurrently

---

##  How to Run

### 1) Start the Server

```bash
python3 server.py
```

###  2) Run a Client (in another terminal)

```bash
python3 client.py
```

###  3) Login Credentials

Update `id_passwd.txt` with:

```
username:password
```

Example:

```
alice:alice123
bob:bobpass
```

---

##  Future Work

-  SSL/TLS Support for secure communication
-  Logging & Auditing of user actions
-  Switch to Thread-based implementation for better efficiency

---

##  Co-Authors

- Vandana J – vandanaj0110@gmail.com  
- Trishita Umapathi – trishitaumapathi@gmail.com  
- Sumukh Acharya – sumukh.acharya@gmail.com
