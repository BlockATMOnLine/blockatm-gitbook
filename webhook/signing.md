---
description: Protecting your sensitive data 
icon: pen-to-square
---
# Request signing

## Checking a Webhook Signature

BlockATM signs the webhook events and requests we send to your endpoints. We do so by including a signature in each event’s BlockATM-Signature-V2 header. 
This allows you to validate that the events and requests were sent by BlockATM , not by a third party.

Before you can verify BlockATM-Signature-V2 signatures for webhook events, you need to retrieve your webhook API key from the Developers page on the BlockATM dashboard.

### Step 1
Concatenate all parameters from the JSON object in ascending order of their keys according to the ASCII character order, 
using the format "key=value" separated by "&"。
Concatenate the 'BlockATM-Request-Time' from the request header in the format '&time=' at the end.

Here is an example of the signature parameters and the resulting signature:

request Data:
```json
{
    "amount":"13.410037",
    "chainId":"5",
    "custNo":"OrderNO_123456",
    "fee":"2",
    "network":"TRON",
    "platOrderNo":"8210000374",
    "status":1,
    "symbol":"USDT",
    "txId":"1t",
    "type":1
}
```

Concatenate the sorted parameters and time result

```java

// you can get the time from request header BlockATM-Request-Time,example of time: 1696946592054
amount=13.410037&chainId=5&custNo=OrderNO_123456&fee=2&network=TRON&platOrderNo=8210000374&status=1&symbol=USDT&txId=1t&type=1&time=1696947336603
```



### Step 2

Compute a HMAC with the SHA-256 hash function. Use your account's webhook API key as the key, and use the signed_payload string as the message in both cases.

```javascript
// you can get the signature from request header BlockATM-Signature-V1
    MEYCIQDHxQ0IhgUNbRqTKbU71fBkp+lAJlMXEQYt6mDQfWRY7gIhAMWIpVoG6qBhgIPi30x30wLlAaxyhptZfm6nMRz75VxA
```
Compare the signature in the header to the expected signature.
