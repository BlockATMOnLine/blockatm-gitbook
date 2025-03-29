# Payout Service



## Step 1: Deploy the Payout Contract

The Payout Contract is a prerequisite for enabling disbursement functionality.

**Deployment Process:**

1. **Connect** to the BlockATM Merchant Dashboard using your administrator address
2. Navigate to the top menu: **Payout Contract** → Click **Create  Payout Contract**
3. Enter:
   * Contract Name
   * Withdraw Address
4. Click **Create** and authorize the deployment through wallet signature

> ℹ️ **Note:**\
> The contract address will be generated upon successful deployment.&#x20;





## Step 2: Upload Payout Orders

You may choose one of the following submission methods:

#### Option 1: API Integration (Recommended)

* Programmatic integration via REST API
* Real-time processing upon submission
* Requires authentication with API keys

Refer to the API Documentation for specifications



#### Option 2: Excel File Upload

* Manual submission by finance staff
* Download the standardized template
* Supports batch processing (multiple orders)

> 📌 **Submission Guidelines:**
>
> * All recipient addresses must be whitelisted
> * Minimum payout amount: $10 equivalent
> * Unique Identifier Mandatory





### Step 3: Submission Payout Orders

#### Process Flow

1. **Authorized treasury personnel** can submit disbursement orders through the admin console
2. **Balance Verification**:
   * System automatically checks contract balance
   * Requires: `Available Balance ≥ Order Amount + Network Fees`
3. **Auto-Execution**:
   * BlockATM processes valid orders automatically
   * Token transfers occur on-chain
   * Typical completion: Within 15 block confirmations

#### Requirements

* Minimum balance buffer: 0.005 ETH (or equivalent for gas)
* Valid KYC status for all recipient addresses
* Unique order reference IDs (no duplicates)

> 🔍 **Status Tracking**\
> Real-time monitoring available via:
>
> * Transaction hash lookup
> * Webhook notifications
> * Dashboard audit logs



### Step 4: Webhook Event Processing

**The final step** is to processing Payout Event via **webhook** and process your business logic based on the results. For details, please refer to the **Webhook Guide**.

