# Request Signing

You signs the requests that send to blockATM server. The request need include api-key in each event’s BlockATM-API-Key header. This allows BlockATM to validate that the requests were sent by Your Server, not by a third party.

### Basic Information&#x20;

* ApiKey    I**E**nclude in each event’s **BlockATM-API-Key** header.&#x20;
* Secret Key    encrypts request parameters,  result placed in the **BlockATM-Signature-V1** header.

You can locate the corresponding API Key within the merchant backend under various integration scenarios (such as the checkout counter or payment delegation contracts).&#x20;

<figure><img src="../../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

### Sign &#x20;

**step 1**&#x20;

Concatenate all parameters from the JSON object in ascending order of their keys according to the ASCII character order, using the format "key=value" separated by "&"。

Original request data:

```
{"custNo":"86000123","orderNo":"202504001399","lang":"zh-CN"}
```

Processed Result:

```
custNo=86000123&lang=zh-CN&orderNo=202504001399
```



**step 2**

Concatenate the '**BlockATM-Request-Time**' from the request header in the format '\&time=' at the end.

&#x20;example **BlockATM-Request-Time =** 1742723373000

Processed Result:

```
custNo=86000123&lang=zh-CN&orderNo=202504001399&time=1742723373000
```



**step 3**&#x20;

Compute a HMAC with the SHA-256 hash function. Use your cashier's  **Secret Key** as the key,

```
Dihl6oOt5UkaHo9sEouquP3EqbukLX2dAOoKTSGicYryTvH1m9r6vtSLHGutZn7u34/06gjhdpbXRFPdjb51GVHvG75qWXZ1P/boL89xtuja6eTEy9q/aS8R270Q1A+m/MOTxdiifCy0IByrSpCs4VJKaj2d8jlJo2GHznsH+q0=
```

\
**Attachment:** **java** **version** [**demo**](https://github.com/CTradeExchange/sign-demo)**.**
