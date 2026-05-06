# Blockchaon Based Supply Chain Traceability Platform

A secure, role-based decentralized supply chain management system built on the Ethereum blockchain. This project utilizes Solidity smart contracts for immutability and tracking, paired with a modern Next.js frontend featuring custom JWT-based authentication and role-based access control.

## 🌟 Key Features

- **Decentralized Tracking**: Monitor the entire lifecycle of products on an immutable ledger.
- **Role-Based Access Control (RBAC)**: Secure role assignment including Admin, Manufacturer, Warehouse, and Retailer.
- **Admin Approval Workflow**: New users must be approved by the Admin before accessing role-specific dashboards.
- **Dual Authentication**: Combines Web3 wallet connection (MetaMask) with traditional JWT/Bcrypt authentication for robust user session management.
- **Real-Time Dashboards**: Distinct, customized dashboard views based on the approved user role.
- **Smart Contract Integration**: Deployed via Hardhat, enabling Web3.js interactions directly from the Next.js App Router client.

## 🛠 Technology Stack

### Frontend (Client)
- **Framework**: Next.js 14 (App Router)
- **Language**: TypeScript
- **Styling**: Tailwind CSS
- **Web3 Interaction**: Web3.js
- **Authentication**: JSON Web Tokens (JWT) & bcryptjs

### Backend (Blockchain)
- **Languages**: Solidity (^0.8.19), TypeScript
- **Environment**: Hardhat
- **Local Blockchain**: Hardhat Node / Ganache

## 📁 Project Structure

The repository is divided into two primary workspaces:

- `backend/`: Contains all Hardhat configurations, Solidity smart contracts, and deployment scripts. Smart contract artifacts are automatically exported to the client.
- `client/`: Contains the Next.js React frontend, API routes for authentication, and the user interface components mapped by role.

## Installation

### Prerequisites

Before you begin, ensure you have the following installed:

- **Node.js** (v18 or higher) - [Download](https://nodejs.org/)
- **Git** - [Download](https://git-scm.com/downloads)
- **Ganache** - [Download](https://trufflesuite.com/ganache/)
- **MetaMask** - [Chrome Extension](https://chrome.google.com/webstore/detail/metamask) | [Firefox Add-on](https://addons.mozilla.org/en-US/firefox/addon/ether-metamask/)
- **VS Code** (Recommended) - [Download](https://code.visualstudio.com/)

### Step 1: Clone the Repository

```bash
git clone https://github.com/faizack619/Supply-Chain-Blockchain.git
cd Supply-Chain-Blockchain
```

### Step 2: Install Dependencies

Install root dependencies (for Hardhat):

```bash
cd backend
npm install
cd ..
```

Install client dependencies:

```bash
cd client
npm install
cd ..
```

### Step 3: Configure Ganache

1. Open Ganache and create a new workspace
2. Note the RPC Server URL (usually `http://127.0.0.1:7545` or `http://127.0.0.1:8545`)
3. Copy the Chain ID (usually `1337` or `5777`)

### Step 4: Configure Hardhat

Update `hardhat.config.ts` with your Ganache network settings:

```typescript
networks: {
  ganache: {
    url: "http://127.0.0.1:7545", // Your Ganache RPC URL
    chainId: 1337, // Your Ganache Chain ID
    accounts: {
      mnemonic: "your ganache mnemonic" // Optional: if using mnemonic
    }
  }
}
```

### Step 5: Deploy Smart Contracts

Compile the smart contracts:

```bash
npx hardhat compile
```

Deploy to Ganache:

```bash
npx hardhat run scripts/deploy.ts --network ganache
```

The deployment script will automatically update `client/src/deployments.json` with the contract address.

### Step 6: Configure MetaMask

1. Open MetaMask and click the network dropdown
2. Select "Add Network" → "Add a network manually"
3. Enter the following details:
   - **Network Name**: Ganache Local
   - **RPC URL**: `http://127.0.0.1:7545` (or your Ganache URL)
   - **Chain ID**: `1337` (or your Ganache Chain ID)
   - **Currency Symbol**: ETH
4. Click "Save"

5. Import an account from Ganache:
   - In Ganache, click the key icon next to an account to reveal the private key
   - In MetaMask, click the account icon → "Import Account"
   - Paste the private key and click "Import"

## Running the Project

### Start Ganache

1. Open Ganache application
2. Create or open a workspace
3. Ensure the server is running

### Deploy Contracts (if not already deployed)

```bash
npx hardhat run scripts/deploy.ts --network ganache
```

### Start the Frontend

```bash
cd client
npm run dev
```

The application will be available at [http://localhost:3000](http://localhost:3000)

### Build for Production

```bash
cd client
npm run build
npm start
```

## 📖 Usage Guide

1. **MetaMask Setup**: Connect your MetaMask wallet to the local network (e.g., Localhost 8545 or Ganache). Import an account using a private key provided by the local node.
2. **Registration**: Navigate to the `/register` page to create a new account, selecting your intended role (Manufacturer, Warehouse, Retailer).
3. **Admin Approval**: 
   - Login as the Admin.
   - Go to the Admin Dashboard / Access Requests page to approve pending user registrations.
4. **Role-Specific Dashboards**:
   - Once approved, users can log in to access their specific dashboard.
   - Each role is restricted to its authorized operational stages.
5. **Product Tracking**: Use the tracking interfaces to view active inventories and trace product journeys across the blockchain.

## 🤝 Contributing
Contributions, issues, and feature requests are welcome!

## 📄 License
This project is licensed under the MIT License.
