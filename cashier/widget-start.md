---
description: Just three  steps to  complete the integration .
icon: plug
---

# Widget SDK

### 1. import

Add the SDK as a script to your HTML file.

```javascript
<script src="https://cashier.blockatm.net/libs/BlockATM.umd.js?apiKey=[API_KEY]"></script>
```

Once you've included this script, you're ready to initialize the Web SDK and start integrating with our suite of cryptocurrency payment solutions.

### 2. Initialize

Initialize the SDK in your application with the flow, variant,lang and any parameters related to deposit cryptocurrency.

```javascript
window.BlockATM.init(dom, {
    custNo: '86000123',
    lang: 'en-US',
    orderNo: "D20250030032"
    callback: ({type})=>{
        if(type==='cancel'){
            // Here is the logic to cancel the payment
        }else if(type==='finish'){
            // Here is the logic to complete the payment
        }
    }
})
```

#### 3. Signing

You need to sign your widget URL before you can display the widget. Learn more about [**URL signing**](can-shu-qian-ming.md).
