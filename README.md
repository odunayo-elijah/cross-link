# CrossLink Protocol

> Next-generation multi-validator Bitcoin-Stacks interoperability solution

[![License](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Clarity](https://img.shields.io/badge/Clarity-2.0-orange.svg)](https://clarity-lang.org/)
[![Stacks](https://img.shields.io/badge/Stacks-Blockchain-purple.svg)](https://stacks.co/)

## Overview

CrossLink Protocol revolutionizes cross-chain asset mobility by providing a decentralized, validator-secured gateway between Bitcoin and Stacks ecosystems. Built with enterprise-grade security patterns, the protocol enables seamless bi-directional asset transfers while maintaining cryptographic integrity through multi-signature validation, threshold consensus mechanisms, and comprehensive fraud protection.

## Features

- ✅ **Multi-Validator Consensus** - Decentralized validator network for transaction verification
- ✅ **Cryptographic Security** - 65-byte signature validation and transaction hash verification
- ✅ **Economic Safety** - Configurable deposit limits and balance tracking
- ✅ **Emergency Controls** - Administrative pause/resume functionality
- ✅ **Fraud Protection** - Comprehensive validation and anti-replay mechanisms
- ✅ **Audit Trail** - Complete transaction history and validator signatures

## Architecture

### Core Components

1. **Validator Network** - Decentralized consensus mechanism for cross-chain verification
2. **Deposit Processing** - Bitcoin transaction registration and confirmation system
3. **Withdrawal Engine** - Secure asset transfer back to Bitcoin network
4. **Balance Management** - User balance tracking within bridge ecosystem
5. **Security Layer** - Multi-signature validation and fraud prevention

### Security Model

- **Multi-Signature Validation**: Requires validator consensus for transaction processing
- **Threshold Confirmations**: Minimum 6 Bitcoin confirmations for security
- **Economic Limits**: Deposit amounts between 0.001 BTC and 10 BTC
- **Anti-Replay Protection**: Transaction hash uniqueness enforcement
- **Emergency Controls**: Administrative pause/resume capabilities

## Contract Interface

### Administrative Functions

#### `initialize-bridge`

Initializes the CrossLink Protocol bridge system.

```clarity
(define-public (initialize-bridge))
```

#### `pause-bridge` / `resume-bridge`

Emergency pause/resume mechanisms for security incidents.

```clarity
(define-public (pause-bridge))
(define-public (resume-bridge))
```

#### `add-validator` / `remove-validator`

Validator network management functions.

```clarity
(define-public (add-validator (validator principal)))
(define-public (remove-validator (validator principal)))
```

### Core Bridge Operations

#### `initiate-deposit`

Registers incoming Bitcoin deposits for cross-chain processing.

```clarity
(define-public (initiate-deposit
  (tx-hash (buff 32))
  (amount uint)
  (recipient principal)
  (btc-sender (buff 33))))
```

#### `confirm-deposit`

Validates and finalizes deposits through multi-signature consensus.

```clarity
(define-public (confirm-deposit
  (tx-hash (buff 32))
  (signature (buff 65))))
```

#### `withdraw`

Executes cross-chain withdrawals to Bitcoin network.

```clarity
(define-public (withdraw
  (amount uint)
  (btc-recipient (buff 34))))
```

### Query Functions

#### `get-deposit`

Retrieves comprehensive deposit information by transaction hash.

```clarity
(define-read-only (get-deposit (tx-hash (buff 32))))
```

#### `get-bridge-status`

Returns current operational status of the bridge protocol.

```clarity
(define-read-only (get-bridge-status))
```

#### `get-validator-status`

Verifies validator authorization status.

```clarity
(define-read-only (get-validator-status (validator principal)))
```

#### `get-bridge-balance`

Returns user's available bridge balance.

```clarity
(define-read-only (get-bridge-balance (user principal)))
```

## Error Codes

| Code | Constant | Description |
|------|----------|-------------|
| 1000 | `ERROR-NOT-AUTHORIZED` | Unauthorized access attempt |
| 1001 | `ERROR-INVALID-AMOUNT` | Invalid transaction amount |
| 1002 | `ERROR-INSUFFICIENT-BALANCE` | Insufficient user balance |
| 1003 | `ERROR-INVALID-BRIDGE-STATUS` | Invalid bridge state |
| 1004 | `ERROR-INVALID-SIGNATURE` | Cryptographic signature validation failed |
| 1005 | `ERROR-ALREADY-PROCESSED` | Transaction already processed |
| 1006 | `ERROR-BRIDGE-PAUSED` | Bridge operations paused |
| 1007 | `ERROR-INVALID-VALIDATOR-ADDRESS` | Invalid validator principal |
| 1008 | `ERROR-INVALID-RECIPIENT-ADDRESS` | Invalid recipient principal |
| 1009 | `ERROR-INVALID-BTC-ADDRESS` | Invalid Bitcoin address format |
| 1010 | `ERROR-INVALID-TX-HASH` | Invalid transaction hash |
| 1011 | `ERROR-INVALID-SIGNATURE-FORMAT` | Invalid signature format |

## Protocol Constants

| Constant | Value | Description |
|----------|-------|-------------|
| `MIN-DEPOSIT-AMOUNT` | 100,000 satoshis | Minimum deposit (0.001 BTC) |
| `MAX-DEPOSIT-AMOUNT` | 1,000,000,000 satoshis | Maximum deposit (10 BTC) |
| `REQUIRED-CONFIRMATIONS` | 6 blocks | Bitcoin confirmation requirement |

## Development

### Prerequisites

- [Clarinet](https://github.com/hirosystems/clarinet) - Stacks development environment
- [Node.js](https://nodejs.org/) - JavaScript runtime for testing
- [Git](https://git-scm.com/) - Version control

### Setup

1. **Clone the repository**

   ```bash
   git clone https://github.com/odunayo-elijah/cross-link.git
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

### Project Structure

```
cross-link/
├── contracts/
│   └── cross-link.clar          # Main protocol contract
├── tests/
│   └── cross-link.test.ts       # Test suite
├── settings/
│   ├── Devnet.toml             # Development configuration
│   ├── Testnet.toml            # Testnet configuration
│   └── Mainnet.toml            # Mainnet configuration
├── Clarinet.toml               # Clarinet configuration
├── package.json                # Node.js dependencies
└── README.md                   # This file
```

### Testing

The project includes comprehensive test coverage for all protocol functions:

```bash
# Run all tests
npm test

# Check contracts only
clarinet check

# Generate coverage report
npm run test:coverage
```

### Deployment

#### Testnet Deployment

1. **Configure Clarinet for testnet**

   ```bash
   clarinet integrate
   ```

2. **Deploy contract**

   ```bash
   clarinet deploy --testnet
   ```

#### Mainnet Deployment

1. **Ensure comprehensive testing**
2. **Security audit completion**
3. **Deploy with production settings**

   ```bash
   clarinet deploy --mainnet
   ```

## Security Considerations

### Validator Security

- Validators must be thoroughly vetted before onboarding
- Multi-signature requirements prevent single points of failure
- Regular validator rotation recommended for security

### Transaction Security

- All Bitcoin transactions require minimum 6 confirmations
- Cryptographic signature validation prevents forgery
- Anti-replay mechanisms prevent double-spending

### Emergency Procedures

- Bridge can be paused immediately during security incidents
- Emergency withdrawal mechanism for critical situations
- Comprehensive audit trail for post-incident analysis

## Contributing

We welcome contributions from the community! Please follow these guidelines:

1. **Fork the repository**
2. **Create a feature branch**: `git checkout -b feature/amazing-feature`
3. **Commit your changes**: `git commit -m 'Add amazing feature'`
4. **Push to the branch**: `git push origin feature/amazing-feature`
5. **Open a Pull Request**

### Code Standards

- Follow Clarity best practices and naming conventions
- Include comprehensive test coverage for new features
- Document all public functions and complex logic
- Ensure all tests pass before submitting PRs

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Roadmap

- [ ] Multi-asset support (STX, SIP-010 tokens)
- [ ] Enhanced validator slashing mechanisms
- [ ] Cross-chain oracle integration
- [ ] Lightning Network compatibility
- [ ] Mobile SDK development
- [ ] Governance token implementation

---

**Disclaimer**: This protocol is experimental software. Use at your own risk. Always conduct thorough testing before mainnet deployment.
