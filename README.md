# Licence Authentication System

This project implements a secure, distributed system for license authentication. It involves multiple components working together to ensure secure communication and verification of user credentials and licenses. Each component is designed with robust cryptographic techniques to enhance security and integrity.

---

## Features

- Secure communication using AES and RSA encryption.
- Authentication of users (policemen) using usernames and hashed passwords.
- Verification of license numbers and providing related personal data.
- Secure time synchronization using a dedicated Time Server.
- Ticket-based authentication using a Ticket Granting Server.

---

## System Overview

The system is divided into the following components:

### 1. **Policeman (`policeman.py`)**
   - Facilitates secure authentication and communication with the Authentication Server, Ticket Granting Server, and Service Provider.
   - Decrypts personal data and receives encrypted images securely.
   - **Key Features**:
     - AES and RSA encryption/decryption.
     - Verifies digital signatures for message integrity.
     - Retrieves and verifies timestamps from the Time Server.

### 2. **Authentication Server (`authentication_server.py`)**
   - Authenticates policemen using usernames and hashed passwords.
   - Generates session keys for secure communication.
   - **Key Features**:
     - Stores and validates hashed passwords.
     - Generates encrypted tickets for the Ticket Granting Server.

### 3. **Ticket Granting Server (`ticket_granting_server.py`)**
   - Generates session keys and tickets for authenticated clients.
   - **Key Features**:
     - Random session key generation.
     - Encrypted ticket creation for communication with the Service Provider.

### 4. **Service Provider (`service_provider.py`)**
   - Verifies license numbers and provides personal data and images to authenticated clients.
   - **Key Features**:
     - Signs and verifies license data.
     - Encrypts and sends sensitive information securely.

### 5. **Time Server (`time_server.py`)**
   - Provides the current time securely to clients.
   - **Key Features**:
     - Uses RSA encryption and digital signatures for time data.
     - Ensures time synchronization for message validity.

---

## Tech Stack

- **Programming Language**: Python
- **Cryptography Libraries**: `pycryptodome`, `fernet`
- **Networking**: `socket`
- **Serialization**: `pickle`
- **Hashing**: `hashlib`

---

## Workflow

1. **Authentication**:
   - Policeman sends credentials to the Authentication Server.
   - Server validates credentials and issues a ticket for the Ticket Granting Server.

2. **Ticket Validation**:
   - Policeman sends the ticket to the Ticket Granting Server.
   - TGS issues a session key and ticket for the Service Provider.

3. **Service Access**:
   - Policeman sends the ticket and session key to the Service Provider.
   - Service Provider validates the ticket, verifies the license, and returns personal data and an encrypted image.

4. **Time Verification**:
   - Time Server provides secure time synchronization for ensuring message validity.

---

## Sample Inputs/Outputs

### Test Case:
**Input**:
```plaintext
Enter Username: police
Enter Password: password123
Enter the licence number you want to verify: XYZ456
```
**Output**:
```plaintext
Name: Kunal Sharma
Date of Birth: 20/02/2002
```
