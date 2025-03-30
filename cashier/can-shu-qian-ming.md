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



### Code examples:

{% tabs %}
{% tab title="JavaScript" %}
```javascript
import crypto from 'crypto';
import { URL } from 'url';

// Configuration - replace with your actual values
const originalUrl = 'https://cashier.blockatm.com?apiKey=pck_payment_my3T68cbuIXf1x3QOEbWtFEfcJPxeBr8wTewDVM&currencyCode=eth&walletAddress=0xde0b295669a9fd93d5f28d9ec85e40f4cb697bae';
const secretKey = 'sck_QOoPSlHDSsgXYeNyTP2i0ug1HKLRjHw9Ug7mCc1Q0';

// Process URL and parameters
const urlObj = new URL(originalUrl);
const params = urlObj.searchParams;

// URL encode all parameter values
params.forEach((v, k) => params.set(k, encodeURIComponent(v)));

// Generate signature using HMAC-SHA256
const signature = crypto.createHmac('sha256', secretKey)
    .update(params.toString())
    .digest('hex');

// Append signature to URL
urlObj.searchParams.set('signature', signature);

console.log('Signed URL:\n' + urlObj.toString());
```
{% endtab %}

{% tab title="java" %}
```java
package com.btm.api.service;

import javax.crypto.Mac;
import javax.crypto.spec.SecretKeySpec;
import java.net.URI;
import java.net.URLEncoder;
import java.nio.charset.StandardCharsets;
import java.util.*;

public class UrlSigner {

    public static void main(String[] args) throws Exception {
        // Configuration
        String originalUrl = "https://cashier.blockatm.com?apiKey=pck_payment_my3T68cbuIXf1x3QOEbWtFEfcJPxeBr8wTewDVM&currencyCode=eth&walletAddress=0xde0b295669a9fd93d5f28d9ec85e40f4cb697bae";
        String secretKey = "sck_QOoPSlHDSsgXYeNyTP2i0ug1HKLRjHw9Ug7mCc1Q0";

        // Process URL and parameters
        String query = new URI(originalUrl).getQuery();
        Map<String, String> params = new LinkedHashMap<>();

        // URL encode parameters
        for (String param : query.split("&")) {
            String[] kv = param.split("=", 2);
            params.put(kv[0], kv.length > 1 ? URLEncoder.encode(kv[1], StandardCharsets.UTF_8.name()) : "");
        }

        // Build query string
        String queryString = String.join("&", params.entrySet().stream()
                .map(e -> e.getKey() + "=" + e.getValue())
                .toArray(String[]::new));

        // Generate and append signature
        String signedUrl = originalUrl + "&signature=" + hmacSha256(secretKey, queryString);
        System.out.println("Signed URL:\n" + signedUrl);
    }

    private static String hmacSha256(String secret, String data) throws Exception {
        Mac mac = Mac.getInstance("HmacSHA256");
        mac.init(new SecretKeySpec(secret.getBytes(StandardCharsets.UTF_8), "HmacSHA256"));
        return bytesToHex(mac.doFinal(data.getBytes(StandardCharsets.UTF_8)));
    }

    private static String bytesToHex(byte[] bytes) {
        StringBuilder sb = new StringBuilder();
        for (byte b : bytes) {
            sb.append(String.format("%02x", b));
        }
        return sb.toString();
    }
}
```
{% endtab %}
{% endtabs %}







#### Signatures Example:

**Secret Key:**

```
sk_ci_QOoPSlHDSsgXYeNyTP2i0ug1HKLRjHw9Ug7mCc1Q0
```



**URL's Param：**

```
apiKey=pk_payment_my3T68cbuIXf1x3QOEbWtFEfcJPxeBr8wTewDVM&t=1742884523932&custNo=C86002201&orderNo=C202503225
```



**Signature Result:**&#x20;

```
ff7fe6e9b2d065390e325457b744a204419204f693cc42c8e079719938bc9bfd
```









