---
description: Protecting your sensitive data
icon: key-skeleton-left-right
---

# Request signing

## Checking a Webhook Signature

BlockATM signs the webhook events and requests we send to your endpoints. We do so by including a signature in each event’s BlockATM-Signature-V2 header.\
This allows you to validate that the events and requests were sent by BlockATM , not by a third party.

Before you can verify BlockATM-Signature-V2 signatures for webhook events, you need to retrieve your webhook API key from the Developers page on the BlockATM dashboard.

### Step 1

Concatenate all parameters from the JSON object in ascending order of their keys according to the ASCII character order,\
using the format "key=value" separated by "&"。\
Concatenate the 'BlockATM-Request-Time' from the request header in the format '\&time=' at the end.

Here is an example of the signature parameters and the resulting signature:

request Data:

```json
{
  "amount": 999,
  "cashierId": 91,
  "chainId": "11155111",
  "custNo": "cust00001",
  "fromAddress": "0xa9e358e33a57e67c9b84618a52f0194c345c8e35",
  "id": 8210003764,
  "network": "Ethereum",
  "status": 9,
  "symbol": "USDT",
  "txId": "0x1da59f33aa6f6b435514126e26d5622c3e377e4762579aa0ac0130139625853d"
}
```

Concatenate the sorted parameters and time result

```java

// you can get the time from request header BlockATM-Request-Time,example of time: 1696946592054
amount=13.410037&chainId=5&custNo=OrderNO_123456&fee=2&network=TRON&platOrderNo=8210000374&status=1&symbol=USDT&txId=1t&type=1&time=1696947336603
```

### Step 2

Compute a HMAC with the SHA-256 hash function. Use your account's webhook API key as the key, and use the signed\_payload string as the message in both cases.

```javascript
// you can get the signature from request header BlockATM-Signature-V1
    MEYCIQDHxQ0IhgUNbRqTKbU71fBkp+lAJlMXEQYt6mDQfWRY7gIhAMWIpVoG6qBhgIPi30x30wLlAaxyhptZfm6nMRz75VxA
```

Compare the signature in the header to the expected signature.


```java
import javax.crypto.Mac;
import javax.crypto.spec.SecretKeySpec;
import java.nio.charset.StandardCharsets;
import java.util.Base64;
import java.util.Map;
import java.util.TreeMap;

/**
 * HMAC-SHA256 Signature Generator
 */
public class SignatureGenerator {

    public static void main(String[] args) {
        // Test parameters (matches documentation example)
        Map<String, String> testParams = createTestParams();
        String requestTime = "1696947336603"; // From BlockATM-Request-Time header
        String apiKey = "test123";            // Replace with your actual API key

        // Step 1: Build signature payload
        String signPayload = buildSignPayload(testParams, requestTime);
        System.out.println("String to be signed:\n" + signPayload + "\n");

        // Step 2: Calculate HMAC-SHA256 signature
        String signature = calculateHmacSha256(apiKey, signPayload);

        // Output results for verification
        System.out.println("Final Signature (Base64): " + signature);
        System.out.println("Final Signature (HEX)   : " + bytesToHex(decodeBase64(signature)));
    }

    // ====================== Core Methods ====================== //

    /**
     * Constructs the signature payload string
     * @param params Request parameters
     * @param requestTime Timestamp from header
     * @return Sorted parameter string with appended timestamp
     */
    public static String buildSignPayload(Map<String, String> params, String requestTime) {
        // TreeMap automatically sorts keys in ASCII order
        Map<String, String> sortedParams = new TreeMap<>(params);

        StringBuilder payload = new StringBuilder();
        sortedParams.forEach((key, value) -> {
            if (payload.length() > 0) payload.append("&");
            payload.append(key).append("=").append(value);
        });
        payload.append("&time=").append(requestTime); // Append timestamp

        return payload.toString();
    }

    /**
     * Calculates HMAC-SHA256 signature
     * @param secret API key
     * @param message Payload string
     * @return Base64-encoded signature
     */
    public static String calculateHmacSha256(String secret, String message) {
        try {
            Mac hmac = Mac.getInstance("HmacSHA256");
            SecretKeySpec keySpec = new SecretKeySpec(
                secret.getBytes(StandardCharsets.UTF_8), 
                "HmacSHA256"
            );
            hmac.init(keySpec);
            byte[] hash = hmac.doFinal(message.getBytes(StandardCharsets.UTF_8));
            return Base64.getEncoder().encodeToString(hash);
        } catch (Exception e) {
            throw new RuntimeException("HMAC calculation failed", e);
        }
    }

    // ====================== Helper Methods ====================== //

    /** Converts byte array to HEX string (for debugging) */
    private static String bytesToHex(byte[] bytes) {
        StringBuilder hex = new StringBuilder();
        for (byte b : bytes) {
            hex.append(String.format("%02x", b));
        }
        return hex.toString();
    }

    /** Decodes Base64 string to byte array */
    private static byte[] decodeBase64(String base64Str) {
        return Base64.getDecoder().decode(base64Str);
    }

    /** Creates test parameters matching documentation example */
    private static Map<String, String> createTestParams() {
        Map<String, String> params = new TreeMap<>();
        params.put("amount", "999");
        params.put("cashierId", "91");
        params.put("chainId", "11155111");
        params.put("custNo", "cust00001");
        params.put("fromAddress", "0xa9e358e33a57e67c9b84618a52f0194c345c8e35");
        params.put("id", "8210003764");
        params.put("network", "Ethereum");
        params.put("status", "9");
        params.put("symbol", "USDT");
        params.put("txId", "0x1da59f33aa6f6b435514126e26d5622c3e377e4762579aa0ac0130139625853d");
        return params;
    }
}
```