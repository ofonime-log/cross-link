# CrossLink Protocol

[![Clarity Version](https://img.shields.io/badge/Clarity-3.0-blue)](https://clarity-lang.org/)
[![License](https://img.shields.io/badge/License-ISC-green)](./LICENSE)
[![Stacks](https://img.shields.io/badge/Stacks-Blockchain-purple)](https://stacks.co/)

> **Next-generation decentralized Bitcoin-Stacks bridge protocol enabling seamless asset transfers with enterprise-grade security and multi-validator consensus.**

## 🌉 Overview

CrossLink Protocol revolutionizes cross-chain interoperability by providing a trustless, validator-governed bridge that connects Bitcoin's robust security with Stacks' smart contract capabilities. The protocol features advanced cryptographic validation, dynamic consensus mechanisms, and fail-safe emergency protocols to ensure maximum security and reliability for institutional and retail users.

### Key Innovations

- **Multi-signature validation** with decentralized validator consensus
- **Real-time transaction monitoring** and automated security checks
- **Seamless asset recovery mechanisms** with emergency protocols
- **Enterprise-grade security** built for scalability
- **Regulatory compliance** design considerations

## 🏗️ Architecture

### Core Components

1. **Bridge Controller** - Main contract managing cross-chain operations
2. **Validator Network** - Decentralized consensus mechanism
3. **Security Layer** - Multi-layered validation and emergency controls
4. **Asset Management** - Balance tracking and withdrawal mechanisms

### Security Features

- ✅ Multi-validator signature requirements (6 confirmations minimum)
- ✅ Emergency pause/resume functionality
- ✅ Cryptographic signature validation
- ✅ Address format validation for Bitcoin and Stacks
- ✅ Amount limits and balance checks
- ✅ Emergency withdrawal capabilities

## 🚀 Quick Start

### Prerequisites

- [Clarinet](https://docs.hiro.so/clarinet) v2.0+
- [Node.js](https://nodejs.org/) v16+
- [Bitcoin Core](https://bitcoin.org/en/download) (for Bitcoin integration)

### Installation

1. **Clone the repository**

   ```bash
   git clone https://github.com/ofonime-log/cross-link.git
   cd cross-link
   ```

2. **Install dependencies**

   ```bash
   npm install
   ```

3. **Check contract syntax**

   ```bash
   clarinet check
   ```

4. **Run tests**

   ```bash
   npm test
   ```

### Development Setup

1. **Start Clarinet console**

   ```bash
   clarinet console
   ```

2. **Deploy contracts locally**

   ```clarity
   ::deploy_contract cross-link ./contracts/cross-link.clar
   ```

3. **Initialize the bridge**

   ```clarity
   (contract-call? .cross-link initialize-bridge)
   ```

## 📋 Usage

### For Bridge Operators

#### Initialize Bridge

```clarity
(contract-call? .cross-link initialize-bridge)
```

#### Add Validator

```clarity
(contract-call? .cross-link add-validator 'ST1VALIDATOR...)
```

#### Emergency Controls

```clarity
;; Pause bridge
(contract-call? .cross-link pause-bridge)

;; Resume bridge
(contract-call? .cross-link resume-bridge)
```

### For Validators

#### Initiate Deposit

```clarity
(contract-call? .cross-link initiate-deposit
  0x1234567890abcdef...  ;; Bitcoin tx hash
  u1000000               ;; Amount in sats
  'ST1RECIPIENT...       ;; Stacks recipient
  0x03abcdef...          ;; Bitcoin sender pubkey
)
```

#### Confirm Deposit

```clarity
(contract-call? .cross-link confirm-deposit
  0x1234567890abcdef...  ;; Bitcoin tx hash
  0x304502210...         ;; ECDSA signature
)
```

### For Users

#### Check Balance

```clarity
(contract-call? .cross-link get-bridge-balance 'ST1USER...)
```

#### Withdraw to Bitcoin

```clarity
(contract-call? .cross-link withdraw
  u500000                ;; Amount to withdraw
  0x1a2b3c4d5e6f...      ;; Bitcoin recipient address
)
```

## 🔧 API Reference

### Public Functions

#### Administrative Functions

| Function | Description | Access |
|----------|-------------|--------|
| `initialize-bridge` | Initialize bridge operations | Contract Deployer |
| `pause-bridge` | Emergency pause all operations | Contract Deployer |
| `resume-bridge` | Resume bridge operations | Contract Deployer |
| `add-validator` | Add new validator to network | Contract Deployer |
| `remove-validator` | Remove validator from network | Contract Deployer |
| `emergency-withdraw` | Emergency asset recovery | Contract Deployer |

#### Bridge Operations

| Function | Description | Access |
|----------|-------------|--------|
| `initiate-deposit` | Start Bitcoin → Stacks transfer | Validators |
| `confirm-deposit` | Confirm cross-chain deposit | Validators |
| `withdraw` | Withdraw Stacks → Bitcoin | Any User |

### Read-Only Functions

| Function | Description | Returns |
|----------|-------------|---------|
| `get-deposit` | Get deposit information | `(optional deposit-info)` |
| `get-bridge-status` | Check if bridge is paused | `bool` |
| `get-validator-status` | Check validator authorization | `bool` |
| `get-bridge-balance` | Get user's bridge balance | `uint` |

### Validation Functions

| Function | Description |
|----------|-------------|
| `is-valid-principal` | Validate Stacks address |
| `is-valid-btc-address` | Validate Bitcoin address |
| `is-valid-tx-hash` | Validate transaction hash |
| `is-valid-signature` | Validate cryptographic signature |
| `validate-deposit-amount` | Check amount within limits |

## 🔒 Security Considerations

### Multi-Layer Security

1. **Consensus Mechanism**: Requires 6+ validator confirmations
2. **Cryptographic Validation**: ECDSA signature verification
3. **Amount Limits**: Min: 100,000 sats, Max: 1B sats
4. **Emergency Controls**: Immediate pause capabilities
5. **Address Validation**: Strict format checking

### Error Handling

The protocol includes comprehensive error handling:

```clarity
ERROR-NOT-AUTHORIZED           (u1000)  ;; Unauthorized access
ERROR-INVALID-AMOUNT          (u1001)  ;; Amount out of bounds
ERROR-INSUFFICIENT-BALANCE    (u1002)  ;; Insufficient funds
ERROR-INVALID-BRIDGE-STATUS   (u1003)  ;; Invalid bridge state
ERROR-INVALID-SIGNATURE       (u1004)  ;; Signature validation failed
ERROR-ALREADY-PROCESSED       (u1005)  ;; Transaction already processed
ERROR-BRIDGE-PAUSED          (u1006)  ;; Bridge is paused
```

## 🧪 Testing

### Run Test Suite

```bash
# Run all tests
npm test

# Run with coverage
npm run test:report

# Watch mode for development
npm run test:watch
```

### Test Categories

- **Unit Tests**: Individual function testing
- **Integration Tests**: Multi-contract interactions
- **Security Tests**: Validation and error handling
- **Performance Tests**: Gas optimization validation

### Sample Test Structure

```typescript
describe("CrossLink Protocol", () => {
  it("should initialize bridge correctly", () => {
    // Test implementation
  });

  it("should validate Bitcoin addresses", () => {
    // Test implementation
  });

  it("should handle emergency pause", () => {
    // Test implementation
  });
});
```

## 🔄 Deployment

### Testnet Deployment

```bash
clarinet deploy --testnet
```

### Mainnet Deployment

```bash
clarinet deploy --mainnet
```

### Configuration Files

- `settings/Devnet.toml` - Local development settings
- `settings/Testnet.toml` - Testnet configuration  
- `settings/Mainnet.toml` - Production configuration

## 📊 Protocol Constants

| Constant | Value | Description |
|----------|--------|-------------|
| `MIN-DEPOSIT-AMOUNT` | 100,000 sats | Minimum bridge amount |
| `MAX-DEPOSIT-AMOUNT` | 1B sats | Maximum bridge amount |
| `REQUIRED-CONFIRMATIONS` | 6 | Validator confirmations needed |

## 🤝 Contributing

We welcome contributions from the community! Please read our contributing guidelines:

1. **Fork** the repository
2. **Create** a feature branch (`git checkout -b feature/amazing-feature`)
3. **Commit** your changes (`git commit -m 'Add amazing feature'`)
4. **Push** to the branch (`git push origin feature/amazing-feature`)
5. **Open** a Pull Request

### Development Guidelines

- Follow Clarity best practices
- Include comprehensive tests
- Document all public functions
- Maintain security standards
- Use semantic commit messages

## 🛣️ Roadmap

### Phase 1: Core Protocol ✅

- [x] Basic bridge functionality
- [x] Multi-validator consensus
- [x] Security controls
- [x] Comprehensive testing

### Phase 2: Enhanced Features 🚧

- [ ] Advanced validator management
- [ ] Governance token integration
- [ ] Enhanced monitoring tools
- [ ] Mobile SDK

### Phase 3: Ecosystem Integration 📋

- [ ] DeFi protocol integrations
- [ ] Lightning Network support
- [ ] Multi-asset support
- [ ] Enterprise APIs

## 📄 License

This project is licensed under the ISC License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- **Stacks Foundation** for blockchain infrastructure
- **Bitcoin Core** development team
- **Clarity Language** contributors
- **Community validators** and early adopters
