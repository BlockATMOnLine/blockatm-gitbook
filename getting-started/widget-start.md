---
icon: bullseye-arrow
---

# 快速开始


1. 引入SDK 

通过一行代码 将SDK引入到您的项目页面中 

```javascript
<script src="https://cashier.blockatm.net/libs/BlockATM.umd.js?apiKey=[API_KEY]"></script>

```

2. 初始化参数 
根据您的项目应用，进行Web SDK参数的初始化 

```javascript
window.BlockATM.init(dom, {
    custNo: '**',
    lang: 'en-US',
    callback: ({type})=>{
        if(type==='cancel'){
            // Here is the logic to cancel the payment
        }else if(type==='finish'){
            // Here is the logic to complete the payment
        }
    }
})
```

