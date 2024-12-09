---
description: >-
  The Deployed factory is decentralized an can be manages from any web3 ui. This
  guide uses the admin
icon: nfc
---

# Manage factory

<figure><img src=".gitbook/assets/-Memex - update.jpg" alt=""><figcaption></figcaption></figure>

## Factory Management and Updates Guide

### ⚠️ Important Permission Notice

**Only the original deployer wallet address can modify factory settings.** If you're using a different wallet address than the one that initially deployed the factory, you won't be able to make any changes.

### Managing Your Factory

#### Available Actions

1. **Withdraw Fees collected deployment fees.**
   * Only the deployer can withdraw accumulated fees
   * Requires transaction confirmation from deployer wallet

#### Update Contract Label

* Factory Name can be updated for local reference
* This is off-chain only and doesn't require a transaction
* Any user can update this for their local interface

#### Deployment Fees

* Only modifiable by original deployer wallet
* Requires on-chain transaction to update

#### Launchpad Configuration Updates

**Modifiable Parameters**

* Virtual Liquidity (Currently 0.3 ETH)
* Pre Bond Target (Currently 0.06 ETH)
* Bonding Target (Currently 0.5 ETH)
* Min Contribution (Currently 0.001 ETH)
* Pool Fees (Currently 0.3%)
* Sell Token Fees (Currently 1%)

**UniswapV3 Addresses**

* Critical infrastructure addresses
* Extreme caution required when modifying
* Incorrect addresses can break functionality

### ⚠️ Critical Update Notice

**Configuration changes only affect future launchpads!**

* Updates DO NOT affect already deployed launchpads
* Existing launchpads retain their original settings
* Only new launchpads will use the updated configuration
* Changes cannot be retroactively applied to existing deployments

### Important Reminders

#### Access Control

1. **Deployer Wallet Required**
   * All on-chain updates must come from the original deployer address
   * Switching to a different wallet won't grant update permissions
   * Keep deployer wallet credentials secure
2. **Transaction Requirements**
   * All updates require to pay miners gas fees
   * Must be signed by deployer wallet



#### If You've Lost Deployer Access

* Factory settings cannot be updated
* New factory deployment would be required
* Existing launchpads continue to function
* Any fees already on the factory will remain stuck.

### Making Updates

1. Connect with deployer wallet
2. Verify you're using correct address
3. Input desired changes
4. Click "Update launchpads config"
5. Confirm transaction in wallet
6. Wait for transaction confirmation

Remember: If you see "Transaction Rejected" or similar errors when trying to update settings, first verify you're connected with the original deployer wallet address.
