---
description: Deploy Contracts → Create Cashier→ Integrate the Cashier->Process Wehook Event
---

# Deposit Service

### Step 1   Deploy Payment Contract&#x20;



1. **Network Connection & Authorization**\
   [In BlockATM DAPP](https://backend.blockatm.net/),Select the target blockchain network for wallet connection and complete authorization in your wallet interface.
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



### Step 2  Create Cashier&#x20;

1. **Access Create Cashier Menu**\
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



### Step 3  Integrate **the Cashier**

Integrate our payment **Cashier**  into your application using the **Widget** . For detailed integration steps, please refer to the [**Integration Guide** ](../cashier/widget-start.md)



### **Step 4.** _Process Results via Webhook_&#x20;

**The final step** is to receive customer payment notifications via **webhook** and process your business logic based on the results. For details, please refer to the [**Webhook Guide**](../webhook/PaymentEvent.md).
