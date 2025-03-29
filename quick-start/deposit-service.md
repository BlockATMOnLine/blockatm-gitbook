---
description: Deploy Contracts → Configure Checkout → Complete Integration
---

# Deposit Service

## Step 1   Deploy Payment Contract&#x20;



1. **Network Connection & Authorization**\
   Select the target blockchain network for wallet connection and complete authorization in your wallet interface.
2. **Navigate to Contract Creation**\
   Under `Receiving Contract` → `Payment Smart Contract` menu, click **Create New Payment Contract**.
3. **Contract Configuration**\
   Enter required parameters:
   * `Contract name` (alphanumeric only)
   * `Finance wallet address` (for fund management)
   * `Withdrawal wallet address` (must differ from finance address)
4. **Deployment Confirmation**\
   Click **Create** and sign the deployment transaction in your wallet:
   * Verify gas fee before signing
   * Keep wallet unlocked until confirmation



## Step 2  Create Cashier&#x20;

1. **Access Creation Menu**\
   Navigate to **Cashier** in top menu → Click **Create New Cashier**&#x20;
2. **Parameter Configuration**\
   Fill in the creation form:
   * `Checkout Name` (Displayed to customers)
   * `Business Logo` (Recommended 256x256px PNG)
   * `Network Selection` (Ethereum/TRON)
   * `Accepted Cryptocurrencies` (Multi-select supported)
   * `Payment Methods` (On-chain/Cross-chain)
3. **Finalize Creation**\
   Click **Confirm** to generate:
   * Unique checkout URL
   * Embeddable widget code
   * API credentials



Step 3.

