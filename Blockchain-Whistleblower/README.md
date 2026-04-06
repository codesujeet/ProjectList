# 🕵️ Blockchain-Based Whistleblower Privacy System

> A secure and anonymous reporting platform leveraging blockchain technology to protect whistleblower identity while ensuring data integrity and tamper-proof evidence storage.

---

## 📑 Table of Contents

- [Overview](#overview)
- [System Design](#system-design)
- [Key Features](#key-features)
- [Technical Approach](#technical-approach)
- [System Workflow](#system-workflow)
- [Privacy Architecture](#privacy-architecture)
- [Outcome](#outcome)
- [Getting Started](#getting-started)
- [Project Structure](#project-structure)
- [License](#license)

---

## Overview

This project provides a **privacy-first reporting platform** that enables individuals to submit sensitive information — such as fraud, corruption, or misconduct reports — while maintaining complete anonymity. By leveraging blockchain technology, the system ensures that submitted data is **immutable and tamper-proof**, while cryptographic techniques guarantee that the reporter's identity remains protected throughout the entire process.

The platform addresses a critical real-world need: protecting those who expose wrongdoing while ensuring the integrity and verifiability of the information they provide.

---

## System Design

```
┌──────────────────────────────────────────────────────────────┐
│                  SUBMISSION LAYER                             │
│   Anonymous Report Form  │  Evidence Upload  │  Metadata     │
└──────────────────────┬───────────────────────────────────────┘
                       │
┌──────────────────────▼───────────────────────────────────────┐
│                  ENCRYPTION LAYER                             │
│   End-to-End Encryption  │  Identity Separation  │  Hashing  │
└──────────────────────┬───────────────────────────────────────┘
                       │
┌──────────────────────▼───────────────────────────────────────┐
│                 BLOCKCHAIN LAYER                              │
│   Immutable Storage  │  Data References  │  Audit Trail      │
└──────────────────────┬───────────────────────────────────────┘
                       │
┌──────────────────────▼───────────────────────────────────────┐
│                VERIFICATION LAYER                             │
│   Data Validation  │  Integrity Check  │  Anonymous Verify   │
└──────────────────────────────────────────────────────────────┘
```

| Layer                | Description                                                    |
| -------------------- | -------------------------------------------------------------- |
| **Submission**       | Anonymous interface for submitting reports and evidence         |
| **Encryption**       | Secures all data before storage; separates identity from data  |
| **Blockchain**       | Stores immutable references to submitted data                  |
| **Verification**     | Enables data validation without revealing reporter identity    |

---

## Key Features

| Feature                                    | Description                                                   |
| ------------------------------------------ | ------------------------------------------------------------- |
| 🔒 **End-to-End Anonymity**               | Reporter identity is never stored or linked to submissions     |
| 🛡️ **Tamper-Proof Storage**               | Blockchain immutability ensures data cannot be altered         |
| 📎 **Secure Evidence Submission**          | Encrypted file uploads for supporting documents                |
| 🔍 **Privacy-Preserving Transparency**    | Verify data integrity without compromising anonymity           |
| 📜 **Immutable Audit Trail**              | Complete, verifiable history of all submissions                |
| 🌐 **Decentralized Trust**                | No single point of failure or authority over the data          |

---

## Technical Approach

### Cryptographic Techniques

| Technique                     | Purpose                                                     |
| ----------------------------- | ----------------------------------------------------------- |
| **Asymmetric Encryption**     | Encrypts report data — only authorized reviewers can decrypt|
| **Hashing (SHA-256)**         | Creates immutable fingerprints of submitted data            |
| **Identity Separation**       | Cryptographically decouples user identity from stored data  |
| **Zero-Knowledge Proofs**     | Enables verification without revealing underlying data      |

### Technology Stack

| Component            | Technology                                              |
| -------------------- | ------------------------------------------------------- |
| **Smart Contracts**  | Blockchain-based data reference storage                 |
| **Encryption**       | AES-256 (data) + RSA (key exchange)                     |
| **Storage**          | Decentralized storage for encrypted evidence            |
| **Backend**          | API layer for submission handling and encryption         |
| **Frontend**         | Anonymous web interface (no tracking, no cookies)       |

### Privacy Design Principles

1. **Data Minimization** — Collect only what is necessary for the report
2. **Identity Separation** — User identity is never stored alongside report data
3. **Encryption by Default** — All data is encrypted before leaving the client
4. **No Logs** — The system does not log IP addresses or user metadata
5. **Decentralized Storage** — No single entity controls the stored data

---

## System Workflow

```
    Reporter                     Platform                    Blockchain
    ────────                     ────────                    ──────────
      │                              │                          │
      │── Submit Report ────────────▶│                          │
      │   (anonymous, encrypted)     │                          │
      │                              │── Encrypt & Process ────▶│
      │                              │── Store Hash ───────────▶│
      │                              │── Store Encrypted Data ─▶│ (IPFS/Decentralized)
      │                              │                          │
      │◀── Receipt Token ───────────│                          │
      │   (anonymous tracking ID)    │                          │
      │                              │                          │
      │                              │                          │
    Reviewer                         │                          │
    ────────                         │                          │
      │── Request Report ───────────▶│                          │
      │                              │── Verify Integrity ─────▶│
      │                              │── Decrypt Data ─────────▶│
      │◀── Verified Report ─────────│                          │
      │   (identity unknown)         │                          │
```

### Submission Flow

1. **Reporter** accesses the anonymous submission portal
2. **Report & evidence** are encrypted client-side before transmission
3. **Encrypted data** is stored on decentralized storage (e.g., IPFS)
4. **Data hash** is recorded on the blockchain for immutability
5. **Receipt token** is provided to the reporter for anonymous follow-up
6. **Identity** is never linked, stored, or logged at any point

---

## Privacy Architecture

```
┌──────────────────────────────────────────────────────────┐
│                   CLIENT SIDE                             │
│                                                          │
│  ┌──────────┐    ┌──────────────┐    ┌───────────────┐  │
│  │  Report   │───▶│  Client-Side │───▶│  Encrypted    │  │
│  │  Input    │    │  Encryption  │    │  Payload      │  │
│  └──────────┘    └──────────────┘    └───────┬───────┘  │
│                                              │          │
└──────────────────────────────────────────────┼──────────┘
                                               │
        ┌──────────────────────────────────────┼──────────┐
        │              SERVER SIDE              │          │
        │                                      │          │
        │  ┌─────────────┐    ┌───────────┐   │          │
        │  │  Hash        │◀──│ Encrypted │◀──┘          │
        │  │  Generation  │    │ Payload   │              │
        │  └──────┬──────┘    └─────┬─────┘              │
        │         │                 │                      │
        │    ┌────▼────┐      ┌────▼──────┐              │
        │    │Blockchain│      │Decentralized│             │
        │    │ (Hash)   │      │  Storage    │             │
        │    └─────────┘      └───────────┘              │
        │                                                  │
        │  ❌ NO identity data stored                     │
        │  ❌ NO IP logging                               │
        │  ❌ NO session tracking                         │
        └──────────────────────────────────────────────────┘
```

---

## Outcome

✅ Provided a **secure mechanism** for reporting sensitive information  
✅ Maintained **strict privacy guarantees** — complete reporter anonymity  
✅ Ensured **data integrity** through blockchain immutability  
✅ Implemented **end-to-end encryption** — data secure from submission to review  
✅ Built a **trustless, decentralized** system with no single point of authority  

---

## Getting Started

### Prerequisites
- Node.js v16+
- Hardhat / Truffle (smart contract development)
- IPFS node (for decentralized storage) — or use Pinata/Infura
- MetaMask or compatible wallet

### Installation
```bash
# Clone the repository
git clone <repository-url>
cd Blockchain-Whistleblower

# Install dependencies
npm install

# Set up environment variables
cp .env.example .env
# Configure blockchain RPC URL, IPFS gateway, etc.
```

### Smart Contract Deployment
```bash
# Compile contracts
npx hardhat compile

# Deploy to local network
npx hardhat node
npx hardhat run scripts/deploy.js --network localhost

# Deploy to testnet
npx hardhat run scripts/deploy.js --network goerli
```

### Run the Application
```bash
# Start the backend
npm run server

# Start the frontend
npm run dev

# Access the anonymous submission portal
# Navigate to http://localhost:3000
```

---

## Project Structure

```
Blockchain-Whistleblower/
├── contracts/                  # Smart contracts
│   ├── WhistleblowerRegistry.sol  # Main registry contract
│   └── interfaces/             # Contract interfaces
├── scripts/                    # Deployment scripts
├── backend/                    # Server-side logic
│   ├── src/
│   │   ├── encryption/         # Encryption & key management
│   │   ├── storage/            # IPFS & decentralized storage
│   │   ├── blockchain/         # Smart contract interaction
│   │   ├── api/                # REST API (anonymous endpoints)
│   │   └── verification/       # Data integrity verification
│   └── package.json
├── frontend/                   # Anonymous web interface
│   ├── src/
│   │   ├── components/         # UI components
│   │   ├── crypto/             # Client-side encryption
│   │   ├── pages/              # Submission & tracking pages
│   │   └── services/           # API interaction
│   └── package.json
├── test/                       # Smart contract & integration tests
├── hardhat.config.js
├── .env.example
└── README.md
```

---

## ⚠️ Important Notice

> This system is designed to facilitate **legitimate and ethical whistleblowing** activities. It should be used responsibly and in compliance with applicable laws and regulations in your jurisdiction.

---

## License

This project is developed for educational and research purposes. Please refer to the `LICENSE` file for details.

---

<p align="center">
  <b>Protecting truth-tellers with the power of blockchain 🕵️🔐</b>
</p>
