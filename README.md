# Memex Launchpad

Memex is a sophisticated decentralized application (dApp) designed for creating and managing token launchpads on EVM-compatible blockchain networks. The platform leverages smart contracts to ensure secure, transparent, and efficient token launches while minimizing deployment costs through innovative clone factory patterns.

## Overview

Memex operates as a full-stack solution combining:

-   Laravel v11.31 backend
-   Vue.js 3.x frontend with Composition API
-   Smart contract infrastructure for EVM networks
-   Web3 authentication system
-   Inertia.js for seamless SPA experience
-   Real-time trading data visualization

## Core Features

-   Automated launchpad creation and management
-   Multi-chain support for EVM-compatible networks
-   Gas-efficient contract deployment via clone factory pattern
-   Web3 wallet authentication
-   Real-time trading charts and statistics
-   Social features including messaging system
-   Token holder tracking and management
-   Comprehensive admin dashboard

## Technical Architecture

### Backend Stack

-   Laravel v11.31
-   MySQL/PostgreSQL database
-   RESTful API architecture
-   Web3 integration for blockchain interactions

### Frontend Stack

-   Vue.js 3.x with Composition API
-   Tailwind CSS 3.x for styling
-   Inertia.js for SPA functionality
-   Shadcn-vue components
-   Trading view integration for charts

### Blockchain Integration

-   EVM-compatible smart contracts
-   Factory pattern implementation
-   Web3 authentication
-   Multi-chain support

## Smart Contract Architecture

### Factory Pattern Implementation

The system employs a factory pattern for contract deployment, which offers several advantages:

1. **Gas Efficiency**: Utilizes clone proxies to reduce deployment costs by up to 60%
2. **Centralized Management**: Factory serves as a hub for all contract deployments
3. **Standardization**: Ensures consistency across all deployed contracts
4. **Cost Control**: Optimizes gas consumption for contract deployment

### Deployment Costs

Gas costs vary by network:

-   Layer 1 networks (e.g., Ethereum): $8-12 USD
-   Layer 2 networks (e.g., Base): $4-6 USD

## Prerequisites

Before deploying Memex, ensure you have:

1. PHP 8.1 or higher
2. Node.js 16+ and npm
3. Composer
4. Access to an EVM-compatible network
5. Web3 wallet for contract deployment
6. MySQL/PostgreSQL database

## Installation

1. Download and unzip the script from codecanyon:

```bash
unzip memex-vps.zip
cd memex-launchpad
```

2. Install PHP dependencies:

```bash
composer install
```

3. Install JavaScript dependencies:

```bash
npm install
```

4. Configure environment variables:

```bash
cp .env.example .env
php artisan key:generate
```

5. Set up the database:

```bash
php artisan migrate
```

6. Deploy factory contract:

-   Choose target network
-   Deploy factory contract using provided scripts
-   Update configuration with factory address

## Factory Contract Deployment

**Important**: A factory contract must be deployed before using the system. This contract:

-   Enables frontend contract deployment functionality
-   Manages deployment configurations
-   Handles fee collection
-   Controls contract creation process

All contracts are verified on network explorers (e.g., BSCScan, BaseScan) for transparency.

## Security Considerations

-   All smart contracts undergo thorough security audits
-   Implements secure Web3 authentication
-   Uses standard security practices for Laravel applications
-   Regular security updates and patches

## Support

This repo will manage support issues for develper related queries and bug reports.

## License

These docs are licensed under the MIT License - see the LICENSE file for details.

## Support

For support, please:

-   Open an issue in the GitHub repository
-   Join our Discord community
-   Contact our support team

## Disclaimer

While Memex implements various security measures, users should conduct their own due diligence when deploying contracts or launching tokens. Gas costs mentioned are approximate and may vary based on network conditions.
