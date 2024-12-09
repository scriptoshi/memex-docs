---
description: This quickstart will get up and running in the fastest route.
icon: gauge-simple-min
---

# Understanding Memex

Memex is a decentralized application (dApp) that operates on EVM-compatible blockchain networks. As a dApp, Memex utilizes smart contracts deployed on the blockchain to handle critical parts of its business logic and operations.



### EVM Contracts

The decentralized contracts are installed via a factory pattern.&#x20;

### Important: Factory Deployment Requirement

Before using the system, you must deploy at least one factory contract to your chosen blockchain. This is a mandatory step that:

* Enables contract deployment functionality in the frontend
* Manages deployment configurations
* Handles deployment fee collection
* Controls the contract creation process
* Please note: All contracts have been verified on bsccan and basescan or equivalent explorer. You can simply follow the deployed factory address on etherscan to view the contract code.

Deploying contracts is expensive in terms of gas. Its to this end that memex uses cheap clones to deploy the contracts. Basically your installation will simply clone an already deployed factory, this saves almost 60% gas needed and should keep deploys cheap for you and your users.  The factory serves as the central hub for all future contract deployments. the latest active factory in each network is used to deploy the launchpad and token contracts. This process is gas intensive and will burn about approx  4-12 USD gas, depending on the gas price and network. The gas cost is dependent on the newtwork . For example ETHEREUM  chain may cost more while L2s like BASE chain will cost less.



**HOW IT ALL WORKS? (Blockchain)**

1. In the admin panel you will deploy the factory contract, with settings based on your site taste
2. In the frontend, users connect to this factory and deploy the token and launchpad. deployement fees are collected by the factory. The setting you made in admin are used to configure the launchpad.
3. In the admin you can withdraw any collected deployement fees anytime.
4. In the Admin You can also modify setting of the factory. Please note setting will only affect future launchpads, whatever is deployed will not change.
5. The created launchpad will  will allow users to buy and sell tokens after they hit 20% of the Virtual ETH amount you set. (Prebonding)
6. The launchpad harvests a fee set by you on token sales.  The fee is sent to your designated address each time a sale occurs. there is no need to withdraw this fee. You can set this address to any you wish.



### Prerequisites

Before getting started with Memex, please ensure you have:

* A Web3 wallet installed and configured - this is mandatory for both administrators and users to interact with the application
* Basic familiarity with blockchain interactions

#### Recommended Web3 Wallets

You can use any of these popular Web3 wallets to interact with Memex:

* [MetaMask](https://metamask.io/download/) (most widely used)
* [Binance Web3 Wallet](https://www.binance.com/en/web3wallet)
* WalletConnect
* Coinbase Wallet
* [Trust Wallet](https://trustwallet.com/)

<figure><img src=".gitbook/assets/Screenshot 2024-12-08 at 7.24.38 PM.png" alt="" width="338"><figcaption></figcaption></figure>

1. &#x20;Metamask ->
2. Binance Wallet ->&#x20;
3. Trus wallet -> [https://trustwallet.com/](https://trustwallet.com/)

## Pre Installation considerations

#### System Requirements

* PHP >= 8.2
* Composer
* Node.js >= 16.x
* MySQL >= 8.0 or PostgreSQL >= 14
* The following PHP extensions:
  * BCMath
  * Ctype
  * JSON
  * Mbstring
  * OpenSSL
  * PDO
  * Tokenizer
  * XML

#### Required API Keys

You'll need to obtain the following API keys:

* CoinCap API Key: Get it from [coincap.io/api-key](https://coincap.io/api-key)
* Project ID: Available at [cloud.reown.com](https://cloud.reown.com/)
* Ankr API Key: Generate at [ankr.com/rpc/projects](https://www.ankr.com/rpc/projects/)

