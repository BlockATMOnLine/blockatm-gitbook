---
icon: key-skeleton-left-right
---

# Url Signing

A signed URL helps limit access from unauthorized third parties by providing limited permissions and time to make a request.\
it must be appended at the end of the URL.

### How to sign URLs

1. Send your widget URL to your backend server.
2. Generate the signature using the secret key found in your BockATM Cashier dashboard.
3. Return either the signature or entire signed URL.
4. Show the widget using the SDK or URL.

### How to generate signatures

1. Create an HMAC (Hash-Based Message Authentication Code) using the SHA-256 hash function

* Use your secret API key as the key
* the original URL's query string as the message.

2. For URL-based integrations, make sure all query parameter values are **URL-encoded** before creating the signature.

Code examples:

```javascript
import crypto from 'crypto';

const originalUrl = 'https://cashier.blockatm.com?apiKey=pk_test_key&currencyCode=eth&walletAddress=0xde0b295669a9fd93d5f28d9ec85e40f4cb697bae';

const signature = crypto
  .createHmac('sha256', 'sk_test_key')  // Use your secret key
  .update(new URL(originalUrl).search)  // Use the query string part of the URL
  .digest('base64');  // Convert the result to a base64 string

const urlWithSignature = `${originalUrl}&signature=${encodeURIComponent(signature)}`;  // Add the signature to the URL

console.log(urlWithSignature);  // Print the signed URL
```
