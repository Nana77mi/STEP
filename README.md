# Client-Side Web Disk System Based on STEP

## Overview
This project implements a **client-side program** for file uploading in a web disk system based on the **Simple Transfer and Exchange Protocol (STEP)** and **TCP (Transmission Control Protocol)**. The system follows the Client/Server (C/S) architecture, enabling secure, efficient file transfer between the client and server.

### Key Features
- **File Uploading**: Upload files from the client to the server, ensuring file integrity with MD5 checks.
- **Authentication**: User login via token-based authentication.
- **Threading for Efficiency**: Implements concurrent programming, thread pools, and packet switching for improved performance.
- **Deletion Operation**: Automatically deletes files with the same key on the server before uploading.
- **Progress Feedback**: Displays upload progress with detailed statistics.

---

## Architecture
### C/S Architecture
- **Client**: Sends user requests (e.g., login, file upload) to the server.
- **Server**: Processes client requests and ensures secure, reliable file storage.

### Workflow
1. User provides the server's IP, username, and file path.
2. The client authenticates using a token-based system.
3. Deletes files with the same key on the server.
4. Sends an upload request and uploads files in blocks, tracking progress.
5. Ensures file integrity using MD5 checksum validation.

---

## Implementation
### Technologies Used
- **Programming Language**: Python 3
- **Libraries**: 
  - `socket`: Network communication.
  - `threading` & `multiprocessing`: Multithreading for efficiency.
  - `hashlib`: Password encryption.
  - `json`: Data serialization.
  - `tqdm`: Progress bar visualization.

### Concurrency
- **Thread-Based Parallelism**: Separate threads handle file upload and response reception, improving execution efficiency.
- **Thread Pool**: Limits the number of threads for better resource management.

### File Transmission
- Files are divided into blocks for efficient uploading.
- Block size is determined by the server, with each block uploaded concurrently.

---

## Testing
### Environment
- **Client**: 1-core processor, 1024MB memory (Ubuntu VM).
- **Server**: 2-core processor, 2048MB memory (Ubuntu VM).

### File Sizes Tested
- **Range**: 132KB to 935KB.

### Results
- A linear relationship was observed between file size and upload time for files smaller than 1MB.
- Bottlenecks identified:
  - Small block size leading to excessive splitting and increased disk I/O.
  - Network latency affecting upload speed.

---

## How to Run
1. Start the server:
   ```bash
   python server.py
   ```
   The server listens on port 1379.

2. Start the client:
   ```bash
   python client.py --server_ip <IP> --id <username> --file <file_path>
   ```
