# PAPA SOL - Advanced Solana Flash Loan Arbitrage Bot

<div align="center">

<a href="https://ibb.co/nMyv9F57"><img src="https://i.ibb.co/nMyv9F57/download-1.jpg" alt="download-1" border="0"></a>

[![CI](https://github.com/SMSDAO/papa-sol-arb/workflows/CI/badge.svg)](https://github.com/SMSDAO/papa-sol-arb/actions)
[![Vercel](https://img.shields.io/badge/vercel-deployed-success)](https://papa-sol-arb.vercel.app)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

*High-frequency automated arbitrage bot with multi-DEX integration and dynamic EWMA adaptation*

</div>

---

## 📋 Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Quick Start](#quick-start)
- [Deploy](#deploy)
- [Usage](#usage)
- [Architecture](#architecture)
- [Troubleshooting](#troubleshooting)
- [Sponsors](#sponsors)
- [License](#license)

---

## 🎯 Overview

**PAPA SOL** is a high-frequency automated arbitrage bot built for Solana that detects and executes triangular flash loan opportunities across multiple DEXs with exceptional speed and accuracy.

### Key Capabilities

- **High-Frequency Auto-Arbitrage**: Continuously scans and executes arbitrage across 12+ triangle paths
- **22 Executions/Second**: Optimized Rust-based engine for maximum throughput
- **Multi-DEX Integration**: 
  - Raydium
  - Orca
  - Meteora
  - Jupiter
- **Dynamic EWMA Adaptation**: Real-time price feed adaptation using Exponential Weighted Moving Average
- **Flash Loan Support**: Atomic transactions with zero capital requirement
- **Real-Time Monitoring**: Web-based admin dashboard with live opportunity tracking

---

## ✨ Features

| Feature | Details |
|---------|---------|
| **Execution Speed** | 22 tx/sec across multi-triangle paths |
| **Triangle Paths** | 12+ concurrent monitoring |
| **DEX Support** | Raydium, Orca, Meteora, Jupiter |
| **Price Adaptation** | Dynamic EWMA for market conditions |
| **Dashboard** | Real-time monitoring UI |
| **Phantom Integration** | Web3 wallet connection |
| **CLI Tools** | Deployment & configuration via PowerShell/Bash |

---

## 🚀 Quick Start

### Prerequisites

- Node.js 18+
- Rust 1.70+
- Solana CLI
- Phantom Wallet (for testing)
- Git

### Installation

1. **Clone the Repository**

```bash
git clone https://github.com/SMSDAO/papa-sol-arb.git D:\solanaremix\papa-sol-arb
cd papa-sol-arb
```

2. **Run Setup Script** (Windows PowerShell)

```powershell
& ./scripts/setup.ps1
```

On macOS/Linux:

```bash
bash scripts/setup.sh
```

3. **Start Development UI**

```bash
cd papa-sol-ui
npm run dev
```

The dashboard will be available at `http://localhost:3000`

---

## 🌐 Deploy

### Prerequisites for Deployment

```bash
# Ensure you have Solana CLI configured
solana config get
# Switch to devnet for testing
solana config set --url devnet
```

### Deployment Steps

1. **Deploy Smart Contracts (Anchor)**

```bash
anchor build
anchor deploy devnet
```

2. **Start Arbitrage Bot**

```bash
cargo run --release bot
```

Monitor output for:
```
✓ Connected to devnet
✓ Loaded 12 triangle paths
✓ Initializing DEX feeds: Raydium, Orca, Meteora, Jupiter
✓ Listening for opportunities...
```

3. **Deploy Web UI to Vercel** (Production)

```bash
vercel --prod
```

Deployment URLs:
- **Primary**: https://papa-sol-arb.vercel.app
- **Primary Alt**: https://papa-sol-arb-git-main-tradeos.vercel.app
- **Secondary**: https://papa-sol-nqjewmfbd-tradeos.vercel.app

---

## 💻 Usage

### Web Dashboard (Admin Panel)

Access the control panel at `http://localhost:3000/admin` or production URLs above.

#### Features:

1. **Phantom Wallet Connection**
   - Click "Connect Wallet" button
   - Approve in Phantom popup
   - Wallet address displayed in top-right

2. **Bot Control**
   - **Toggle Bot**: Switch arbitrage engine on/off
   - **Live Status**: Real-time connection indicator
   - **Triangle Monitor**: View all 12+ active paths
   - **Opportunity Feed**: Stream of detected arbitrage opportunities

3. **Performance Metrics**
   - Execution rate (target: 22 tx/sec)
   - Total opportunities detected
   - Successful trades executed
   - Average profit per execution
   - 24h volume traded

### CLI Commands

```bash
# Check bot status
cargo run -- bot status

# View active triangles
cargo run -- paths list

# Monitor live feed
cargo run -- monitor feed

# Configuration
cargo run -- config set --max-slippage 1.0
cargo run -- config set --min-profit-threshold 0.5
```

---

## 🏗️ Architecture

### Component Overview

```
┌─────────────────────────────────────────┐
│        PAPA SOL Arbitrage Engine        │
├─────────────────────────────────────────┤
│                                         │
│  ┌──────────────────────────────────┐   │
│  │   Multi-DEX Price Feed           │   │
│  │  (Raydium/Orca/Meteora/Jupiter)  │   │
│  └──────────────────────────────────┘   │
│           ↓                              │
│  ┌──────────────────────────────────┐   │
│  │  12+ Triangle Path Scanner       │   │
│  │  (EWMA Dynamic Adaptation)       │   │
│  └──────────────────────────────────┘   │
│           ↓                              │
│  ┌──────────────────────────────────┐   │
│  │  Opportunity Validator           │   │
│  │  & Profit Calculator             │   │
│  └──────────────────────────────────┘   │
│           ↓                              │
│  ┌──────────────────────────────────┐   │
│  │  Flash Loan Executor (22 tx/sec) │   │
│  │  & Settlement Manager            │   │
│  └──────────────────────────────────┘   │
│                                         │
└─────────────────────────────────────────┘
         ↓              ↓
    ┌────────────────────────┐
    │  Web Dashboard (UI)    │
    │  Admin @ :3000/admin   │
    └────────────────────────┘
```

### Tech Stack

- **Backend**: Rust + Anchor Framework
- **Frontend**: Next.js + React
- **Blockchain**: Solana (devnet/mainnet)
- **State Management**: Redux
- **Styling**: Tailwind CSS
- **Deployment**: Vercel

---

## 🔧 Troubleshooting

### Zero Errors - Code Quality Check

#### Rust Code Linting

```bash
# Run clippy for Rust code
cargo clippy

# Expected output: no warnings
```

#### Node.js Dependencies Audit

```bash
# Check for npm vulnerabilities
npm audit

# Fix vulnerabilities automatically
npm audit fix
```

### Common Issues

#### ❌ Issue: "Connection refused" to Solana RPC

```bash
# Solution: Verify network configuration
solana config get
solana config set --url devnet  # or your RPC endpoint
```

#### ❌ Issue: "Insufficient gas" for contract deployment

```bash
# Solution: Ensure devnet account has SOL
solana airdrop 2
```

#### ❌ Issue: Phantom wallet not connecting

```bash
# Solution:
1. Ensure Phantom extension is installed
2. Switch Phantom to Devnet
3. Clear browser cache
4. Reload http://localhost:3000/admin
```

#### ❌ Issue: Triangle paths not detected

```bash
# Solution: Verify DEX integration
cargo run -- paths list
# Should show: ✓ Raydium, ✓ Orca, ✓ Meteora, ✓ Jupiter
```

#### ❌ Issue: Low execution rate

```bash
# Solution: Check performance metrics and optimize
cargo run -- bot status
# Verify 22 tx/sec baseline is maintained
```

---

## 💰 Sponsors & Support

### Support PAPA SOL Development

We welcome contributions and sponsorships to accelerate development!

#### 🔗 Donate via GitHub

[![Sponsor](https://img.shields.io/badge/sponsor-%E2%9D%A4-green?logo=github)](https://github.com/sponsors/SMSDAO)

#### 💸 Donate SOL

Send SOL to support PAPA SOL development:

```
J7bNrvf26uiWWg8sM43eQMwunaPgmvi7pdRC55CnebPE
```

**QR Code for Mobile Donations:**

![Solana Donation QR Code](data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMjAwIiBoZWlnaHQ9IjIwMCIgdmlld0JveD0iMCAwIDIwMCAyMDAiIHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8yMDAwL3N2ZyI+PHJlY3Qgd2lkdGg9IjIwMCIgaGVpZ2h0PSIyMDAiIGZpbGw9IiNGRkYiLz48cmVjdCB4PSI4IiB5PSI4IiB3aWR0aD0iMTgiIGhlaWdodD0iMTgiIGZpbGw9IiMwMDAiLz48cmVjdCB4PSI4IiB5PSIzMiIgd2lkdGg9IjI3IiBoZWlnaHQ9IjI3IiBmaWxsPSIjMDAwIi8+PHJlY3QgeD0iOCIgeT0iNjUiIHdpZHRoPSI4IiBoZWlnaHQ9IjgiIGZpbGw9IiMwMDAiLz48cmVjdCB4PSIyMyIgeT0iNjUiIHdpZHRoPSI4IiBoZWlnaHQ9IjgiIGZpbGw9IiMwMDAiLz48cmVjdCB4PSI2NSIgeT0iOCIgd2lkdGg9IjI3IiBoZWlnaHQ9IjI3IiBmaWxsPSIjMDAwIi8+PHJlY3QgeD0iNjUiIHk9IjQwIiB3aWR0aD0iOCIgaGVpZ2h0PSI4IiBmaWxsPSIjMDAwIi8+PHJlY3QgeD0iODMiIHk9IjQwIiB3aWR0aD0iOCIgaGVpZ2h0PSI4IiBmaWxsPSIjMDAwIi8+PHRleHQgeD0iMTAwIiB5PSIyMDAiIGZvbnQtc2l6ZT0iMTAiIGZpbGw9IiMwMDAiIHRleHQtYW5jaG9yPSJtaWRkbGUiPkRvbmF0ZSBTT0w8L3RleHQ+PC9zdmc+)

**Note:** Replace QR code with actual QR code image generated from the SOL address using a QR code generator (e.g., https://qr-server.com/api/qr)

### Contributors

We thank all contributors who've helped make PAPA SOL possible!

---

## 📄 License

This project is licensed under the **MIT License** - see the [LICENSE](LICENSE) file for details.

---

## 🤝 Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

---

## 📞 Support & Contact

- **GitHub Issues**: [Report bugs or request features](https://github.com/SMSDAO/papa-sol-arb/issues)
- **Discord**: Join our community (coming soon)
- **Email**: contact@papa-sol.dev

---

<div align="center">

**Made with ❤️ by SMSDAO**

*PAPA SOL: Flash Loan Arbitrage on Solana*

Last Updated: December 6, 2025

</div>
