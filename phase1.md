# Phase 1: Foundation - Technical Specification

## 1. Core Smart Contract Development
### Technology Stack
#### Blockchain
- Ethereum

#### Backend
- Smart Contracts: Solidity ^0.8.20
- Development Framework: Hardhat

#### Frontend
- Framework: Next.js 14 with TypeScript
- Web3 Library: ethers.js v6
- State Management: Redux Toolkit
- UI Components: tailwindcss
- Contract Interaction: ethers.js v6

#### Testing
- Testing Framework: Mocha/Chai with Waffle

### Basic Backend Swap Contract (Priority)
#### Core Features
- Simple token-to-token and ETH-to-token swaps: swap tokens for tokens and ETH for tokens
- Single unified fee (0.3%): a fee is charged for each swap
- Basic slippage protection: a slippage parameter is used to prevent the price from changing too much
- Gas-optimized operations: the contract is designed to minimize gas usage

#### Key Functions
- `swapExactTokensForTokens`: Swap tokens for tokens
- `swapExactETHForTokens`: Swap ETH for tokens
- `swapExactTokensForETH`: Swap tokens for ETH
- `getAmountOut`: Calculate the amount of tokens received for a given amount of tokens
- `getFeeAmount`: Calculate the 0.3% fee for a given amount of tokens
- `pause`: Pause the contract
- `unpause`: Unpause the contract

### Security Features
- Reentrancy guards: prevent malicious from starting a swap before the previous swap is complete
- Overflow protection (Solidity ^0.8.x): prevent integer overflow/underflow
- Pausable functionality: pause the contract in case of emergency, allows contract owners to freeze all transactions if something goes wrong
- Basic access control: controls who can do what in the contract

### Error Handling
- Swap execution status events
- Error events for failed transactions
- Price impact calculations

## 2. Frontend Development
### Technology Stack
- Framework: Next.js 14 with TypeScript
- Web3 Library: ethers.js v6
- State Management: Redux Toolkit
- UI Components: tailwindcss

### Core Features
- Wallet Integration
    - Connect wallet (MetaMask integration)
    - Account balance display
    - Network status monitoring
- Swap Interface
    - Token selection interface: allows users to select the tokens they want to swap
    - Token balance display
    - Swap amount input: allows users to input the amount of tokens they want to swap
    - Price impact calculation display
- Transaction Management
    - Basic slippage settings (0.5%, 1%, 2%): allows users to set the slippage they are willing to accept
    - Transaction status tracking: allows users to track the status of their transaction
    - Transaction history display
- Error Handling
    - User-friendly error messages
    - Error handling for failed transactions
    - Transaction failure recovery
### Security Features
- Input Validation & Sanitization
    - Client-side validation for all user inputs
    - Protection against XSS attacks
    - Rate limiting for API calls
- Wallet Security
    - Secure wallet connection handling
    - Session timeout management
    - Clear sensitive data on disconnect
- Transaction Safety
    - Double confirmation for large transactions
    - Warning systems for suspicious token contracts
    - Token allowance safety checks
- Network Security
    - SSL/TLS encryption for all API calls
    - Protection against MITM attacks
    - Secure RPC endpoint handling

## 3. Testing Strategy
### Local Testing (Priority)
- Environment: Hardhat Network
- Unit tests for all swap functions
- Integration tests for contract interactions
- Frontend component testing with Jest
- E2E testing with Cypress

### Testnet Deployment
- Network: Sepolia (Ethereum Testnet)
- Test tokens deployment
- Contract verification on Etherscan

## 4. Future Features (Post Phase 1)
### Liquidity Provision
- Add/remove liquidity: allows users to add or remove liquidity to a pool
- Pool share calculation: allows users to calculate the amount of tokens they would receive for a given amount of liquidity
- Returns visualization: allows users to visualize the returns they would receive for a given amount of liquidity

### Advanced Features
- Multiple fee tiers: allows users to set different fee tiers for different pools
- Flash swaps: allows users to swap tokens without locking up their funds
- Multi-hop routing: allows users to swap tokens in multiple hops
- MEV protection: allows users to protect themselves from MEV

## 5. Success Criteria
1. Successful token swaps on local testnet
2. Working frontend interface
3. 95%+ test coverage for core functions
4. Successful Sepolia deployment
5. Basic documentation complete
6. No critical security issues

## 6. Documentation Requirements
- Smart contract architecture
- API specifications
- Setup instructions
- Testing procedures
- Deployment guide

## Enhanced Project Structure

### 1. Contracts Directory (`contracts/`)

#### Ethereum Directory
- Core contracts in `ethereum/core/`
  - BasicSwap.sol - Main swap functionality
  - BasicSwapPair.sol - Swap logic and liquidity management
  - BasicSwapFactory.sol - Trading pairs management
  - BasicSwapRouter.sol - Trade routing and user interactions
  - BasicSwapRouterFactory.sol - Trading pairs creation and management

- Interfaces in `ethereum/interfaces/`
  - IBasicSwap.sol
  - IBasicSwapFactory.sol
  - IBasicSwapRouter.sol
  - IBasicSwapRouterFactory.sol

- Utilities in `ethereum/utils/`
  - Math.sol
  - SafeMath.sol
  - TransferHelper.sol

#### Tezos Directory
- Core contracts in `tezos/core/`
  - basic_swap.mligo
  - basic_swap_pair.mligo
  - basic_swap_factory.mligo
- Interfaces in `tezos/interfaces/`
- Utilities in `tezos/utils/`

#### Polkadot Directory
- Core contracts in `polkadot/core/`
  - basic_swap.rs
  - lib.rs
- Interfaces in `polkadot/interfaces/`
- Utilities in `polkadot/utils/`

#### Common Directory
- Interfaces in `common/interfaces/`
  - ISwap.sol - Generic swap interface
  - IFactory.sol - Generic factory interface
  - IRouter.sol - Generic router interface
- Utilities in `common/utils/`
  - CommonMath.sol
  - SecurityUtils.sol

### 2. Frontend Directory (`frontend/`)

#### Source Directory (`src/`)
- Components
  - Common components in `components/common/`
  - Swap components in `components/swap/`
  - Wallet components in `components/wallet/`
  - Chain-specific components in `components/chains/`
    - Ethereum components
    - Tezos components
    - Polkadot components

- Hooks
  - useEthereum.ts
  - useTezos.ts
  - usePolkadot.ts

- Services
  - Blockchain services in `services/blockchain/`
    - Ethereum services (swap.service.ts, wallet.service.ts)
    - Tezos services
    - Polkadot services
  - API services in `services/api/`

- Store
  - Chain-specific state management in `store/slices/chains/`

- Configuration
  - Chain configurations in `config/chains/`
    - ethereum.ts
    - tezos.ts
    - polkadot.ts

- Utilities
  - Chain-specific utilities in `utils/chains/`

### 3. Backend Directory (`backend/`)

#### Source Directory (`src/`)
- Modules
  - Ethereum module
    - Services
    - Controllers
    - Repositories
  - Tezos module
  - Polkadot module

- Common
  - Interfaces
  - Utilities

- Configuration

### 4. Test Directory (`test/`)

#### Contract Tests
- Ethereum tests
  - Unit tests
  - Integration tests
- Tezos tests
- Polkadot tests

#### Frontend Tests
- End-to-end tests

#### Backend Tests
- Unit tests
- Integration tests

### 5. Scripts Directory (`scripts/`)

#### Deployment Scripts
- Ethereum deployment scripts
- Tezos deployment scripts
- Polkadot deployment scripts

#### Utility Scripts

### 6. Documentation Directory (`docs/`)

#### Chain-specific Documentation
- Ethereum documentation
- Tezos documentation
- Polkadot documentation

#### API Documentation
#### Deployment Guides
#### Architecture Documentation

