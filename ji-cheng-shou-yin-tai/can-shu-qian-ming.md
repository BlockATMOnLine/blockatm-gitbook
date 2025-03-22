---
icon: pen-field
---

# 参数签名

经过签名的URL通过提供鉴权和请求的时间来限制未经授权的第三方的访问。如果您的Wedgit URL未包括业务订单编号(orderNo)，则强制建议使用signature参数。它必须附加在URL的末尾。



### URL 签名

1. 将您的URL参数发送到您的后端服务。
2. 后端服务使用对接密钥对请求参数进行签名

&#x20; （对接密钥可以在BlockATM收银台对接信息中找到）

3. 后端服务返回签名结果，通过wedgit打开收银台&#x20;





### 生成签名&#x20;

1. 使用 HMAC 和 SHA-256 哈希函数生成签名。

* Key 为收银台的对接密钥
* Message为url完整的字符串参数&#x20;

2. 在签名前，注意对整个参数进行URL-encoded



参考下面示例：

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

