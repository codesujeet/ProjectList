# 💰 Blockchain-Based Escrow System

> A decentralized escrow system powered by smart contracts, extended with fiat payment integration (Razorpay) and real-time order tracking — bridging traditional finance with Web3 infrastructure.

---

## 📑 Table of Contents

- [Overview](#overview)
- [System Architecture](#system-architecture)
- [Core Workflow](#core-workflow)
- [Key Features](#key-features)
- [Technical Details](#technical-details)
- [System Flow Diagram](#system-flow-diagram)
- [Outcome](#outcome)
- [Getting Started](#getting-started)
- [Project Structure](#project-structure)
- [License](#license)

---

## Overview

This project implements a **hybrid escrow system** that combines the security and trustlessness of blockchain smart contracts with the accessibility of traditional fiat payment systems. Users can initiate transactions using familiar payment methods (INR via Razorpay), while the underlying escrow logic is enforced by tamper-proof smart contracts on the blockchain.

The system also includes **real-time order and courier tracking**, making it suitable for e-commerce-like workflows where payment release is conditional on delivery confirmation.

---

## System Architecture

The platform combines **Web2** and **Web3** components into a unified transaction flow:

```
┌──────────────────────────────────────────────────────────────┐
│                   FIAT PAYMENT LAYER                          │
│          Razorpay Integration  │  INR Transactions           │
└──────────────────────┬───────────────────────────────────────┘
                       │
┌──────────────────────▼───────────────────────────────────────┐
│                  CONVERSION LAYER                             │
│         Fiat-to-Crypto Mapping  │  Escrow Locking            │
└──────────────────────┬───────────────────────────────────────┘
                       │
┌──────────────────────▼───────────────────────────────────────┐
│                 BLOCKCHAIN LAYER                              │
│       Smart Contracts  │  Escrow Logic  │  Fund Management   │
└──────────────────────┬───────────────────────────────────────┘
                       │
┌──────────────────────▼───────────────────────────────────────┐
│                  TRACKING LAYER                               │
│    Order Management  │  Courier Integration  │  Status API   │
└──────────────────────┬───────────────────────────────────────┘
                       │
┌──────────────────────▼───────────────────────────────────────┐
│                  USER INTERFACE                               │
│  Transaction Init  │  Status Tracking  │  Confirmations      │
└──────────────────────────────────────────────────────────────┘
```

| Layer                | Description                                                  |
| -------------------- | ------------------------------------------------------------ |
| **Fiat Payment**     | Razorpay integration for INR-based transactions              |
| **Conversion**       | Maps fiat payments to blockchain-backed escrow contracts     |
| **Blockchain**       | Smart contracts for escrow logic and conditional fund release|
| **Tracking**         | Real-time order and courier tracking system                  |
| **User Interface**   | Transaction initiation, status tracking, and confirmations   |

---

## Core Workflow

```
┌─────────────────────────────────────────────────────────────────────┐
│                                                                     │
│  1. User initiates payment via Razorpay (fiat/INR)                 │
│     │                                                               │
│  2. System maps payment → blockchain escrow contract               │
│     │                                                               │
│  3. Funds are logically locked in smart contract                   │
│     │                                                               │
│  4. Order processing & courier tracking begins                     │
│     │                                                               │
│  5. Real-time status updates reflected in system                   │
│     │                                                               │
│  6. Delivery confirmed → smart contract releases funds             │
│                                                                     │
└─────────────────────────────────────────────────────────────────────┘
```

### State Machine

```
    ┌─────────────┐
    │  INITIATED  │ ◀── User makes fiat payment
    └──────┬──────┘
           │
    ┌──────▼──────┐
    │   LOCKED    │ ◀── Funds locked in escrow contract
    └──────┬──────┘
           │
    ┌──────▼──────┐
    │  SHIPPED    │ ◀── Order dispatched, tracking active
    └──────┬──────┘
           │
    ┌──────▼──────┐
    │ DELIVERED   │ ◀── Delivery confirmed
    └──────┬──────┘
           │
    ┌──────▼──────┐
    │  RELEASED   │ ◀── Smart contract releases funds to seller
    └─────────────┘
```

---

## Key Features

| Feature                                    | Description                                                   |
| ------------------------------------------ | ------------------------------------------------------------- |
| 💳 **Fiat to Blockchain Integration**      | Transact using traditional payment methods with blockchain security |
| 🔐 **Smart Contract Escrow**              | Automated, tamper-proof fund locking and conditional release   |
| 📦 **Real-Time Order Tracking**           | Tracks delivery lifecycle with live status updates             |
| 🔍 **Transparent Transaction Flow**       | All actions verifiable and auditable on the blockchain         |
| ⚖️ **Trustless Execution**                | Eliminates dependency on intermediaries                        |
| 🔄 **Hybrid Architecture**               | Best of Web2 (usability) + Web3 (security & trust)            |

---

## Technical Details

| Component            | Technology / Specification                              |
| -------------------- | ------------------------------------------------------- |
| **Smart Contracts**  | Solidity — escrow logic and conditional execution       |
| **Payment Gateway**  | Razorpay API — fiat (INR) payment processing            |
| **Backend**          | Transaction mapping, state management, webhook handling |
| **Order Tracking**   | Courier APIs/webhooks for real-time delivery updates    |
| **Blockchain**       | Ethereum-compatible network                             |
| **Architecture**     | Hybrid — centralized services + decentralized execution |

### Smart Contract Functions

```solidity
// Simplified escrow contract interface
contract Escrow {
    function createEscrow(address seller, uint256 amount) external;
    function lockFunds(uint256 escrowId) external payable;
    function confirmDelivery(uint256 escrowId) external;
    function releaseFunds(uint256 escrowId) external;
    function refund(uint256 escrowId) external;
    function getEscrowStatus(uint256 escrowId) external view returns (Status);
}
```

---

## System Flow Diagram

```
    Buyer                    Platform                   Blockchain          Seller
    ─────                    ────────                   ──────────          ──────
      │                          │                          │                  │
      │── Pay via Razorpay ─────▶│                          │                  │
      │                          │── Create Escrow ────────▶│                  │
      │                          │── Lock Funds ───────────▶│                  │
      │                          │                          │                  │
      │                          │── Process Order ────────────────────────────▶│
      │                          │                          │                  │
      │◀── Tracking Updates ────│◀── Courier Webhook ──────│                  │
      │                          │                          │                  │
      │── Confirm Delivery ─────▶│                          │                  │
      │                          │── Release Funds ────────▶│                  │
      │                          │                          │── Pay Seller ───▶│
      │                          │                          │                  │
```

---

## Outcome

✅ Successfully demonstrated a **practical hybrid escrow system**  
✅ **Bridges fiat payments** (Razorpay/INR) with blockchain smart contracts  
✅ Supports **real-world e-commerce workflows** with order tracking  
✅ Enhances **trust, transparency, and automation** in transactions  
✅ **Trustless execution** — no intermediary dependency  

---

## Getting Started

### Prerequisites
- Node.js v16+
- npm or yarn
- Hardhat / Truffle (for smart contract development)
- Razorpay account (API keys)
- MetaMask or compatible wallet (for blockchain interaction)

### Installation
```bash
# Clone the repository
git clone <repository-url>
cd Blockchain-Escrow-System

# Install dependencies
npm install

# Set up environment variables
cp .env.example .env
# Edit .env with your Razorpay API keys, blockchain RPC URL, etc.
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
# Start the backend server
npm run server

# Start the frontend
npm run dev

# Access the application
# Navigate to http://localhost:3000
```

### Environment Variables
```env
# .env
RAZORPAY_KEY_ID=your_razorpay_key
RAZORPAY_KEY_SECRET=your_razorpay_secret
BLOCKCHAIN_RPC_URL=http://localhost:8545
CONTRACT_ADDRESS=0x...
PRIVATE_KEY=0x...
COURIER_API_KEY=your_courier_api_key
```

---

## Project Structure

```
Blockchain-Escrow-System/
├── contracts/                  # Smart contracts (Solidity)
│   ├── Escrow.sol              # Main escrow contract
│   └── interfaces/             # Contract interfaces
├── scripts/                    # Deployment & interaction scripts
│   ├── deploy.js               # Contract deployment
│   └── interact.js             # Contract interaction helpers
├── backend/                    # Backend server
│   ├── src/
│   │   ├── payment/            # Razorpay integration
│   │   ├── blockchain/         # Smart contract interaction
│   │   ├── tracking/           # Order & courier tracking
│   │   ├── api/                # REST API endpoints
│   │   └── webhooks/           # Payment & delivery webhooks
│   └── package.json
├── frontend/                   # User interface
│   ├── src/
│   │   ├── components/         # UI components
│   │   ├── pages/              # Application pages
│   │   └── services/           # API & blockchain services
│   └── package.json
├── test/                       # Smart contract & integration tests
├── hardhat.config.js           # Hardhat configuration
├── .env.example                # Environment variable template
└── README.md
```

---

## License

This project is developed for educational and research purposes. Please refer to the `LICENSE` file for details.

---

<p align="center">
  <b>Trustless transactions for the real world 🔗💰</b>
</p>
