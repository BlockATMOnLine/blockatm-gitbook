---
description: 只需要三步，轻松完成集成开发
icon: bullseye-arrow
---

# 轻松接入

1. **引入SDK**

通过一行代码 将SDK引入到您的项目页面中

```javascript
<script src="https://cashier.blockatm.net/libs/BlockATM.umd.js"></script>

```





2. **初始化参数**



根据您的项目应用，进行Web SDK参数的初始化，比如客户编号、订单编号、语言等。

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



#### 3. 参数签名



如果您的收银台参数中没有包括orderNo,那么需要对您的url params进行签名。 具体规则见：url 签名
