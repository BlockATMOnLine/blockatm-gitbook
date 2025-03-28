---
description: Deploy Contracts → Configure Checkout → Complete Integration
---

# Deposit Service

## Cryptocurrency Payment Contract Setup Guide

### Step-by-Step Instructions

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

### Technical Notes

* **EVM Chains** (Ethereum/Arbtrium): Requires 0.05+ ETH  gas reserve
* **TRON**: Requires 500+ frozen TRX for bandwidth
* Contract parameters become immutable after deployment

### Visual Guide

```markup
graph TD
    A[1. Select Network] --> B[2. Create Contract]
    B --> C[3. Enter Parameters]
    C --> D[4. Sign & Deploy]
```

