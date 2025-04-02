---
icon: arrows-to-circle
---

# Migration

## 新版版本升级指南（V2）

**目标**：帮助商户快速定位改动点，减少接入成本。





<table><thead><tr><th width="105.78790283203125">功能模块</th><th>变更类型</th><th>具体调整内容</th><th>商户应对措施</th></tr></thead><tbody><tr><td><strong>连钱包支付</strong></td><td>参数校验增强</td><td>1. <code>custno</code> 字段改为必填<br>2. URL参数签名从可选调整为强制（使用HMAC-SHA256）<br></td><td>1. 检查代码是否传递custNo<br>2. 集成签名逻辑（参考<br><a href="https://www.notion.so/BTM-V5-0-0-1839e777a9dc80e08246c4d6d40205f8?pvs=21">签名文档</a>）</td></tr><tr><td><strong>二维码支付</strong></td><td>对接方式重构</td><td>从API生单改为Widget集成（需前端嵌入）</td><td>1. 移除原有API调用<br>2. 集成新Widget（参考<br><a href="https://www.notion.so/BTM-V5-0-0-1839e777a9dc80e08246c4d6d40205f8?pvs=21">Widget集成指南</a>）</td></tr><tr><td><strong>付款功能</strong></td><td>功能扩展</td><td>新增API接口：<code>POST</code> /api/v2/payout/order</td><td>1. 可选迁移至API（推荐）<br>2. 仍支持商户通过Excel上传<br></td></tr><tr><td><strong>Webhook</strong></td><td>算法与字段调整</td><td>1. 签名方式未变更，签名算法调整为HMAC-SHA256<br>2. status 字段由int 类型调整为字符串<br></td><td>1. 更新验签逻辑 （参考<a href="https://www.notion.so/BTM-V5-0-0-1839e777a9dc80e08246c4d6d40205f8?pvs=21">签名文档</a>）<br>2. 适配新字段（<br><a href="https://www.notion.so/BTM-V5-0-0-1839e777a9dc80e08246c4d6d40205f8?pvs=21">字段映射表</a>）</td></tr><tr><td><strong>API接口</strong></td><td>版本升级</td><td>openApi 升级为/v2版本，部分接口逻辑调整，详情见下面列表：<br><br></td><td></td></tr><tr><td></td><td>获取支持的网络</td><td>由原路径：/api/v1/public/networklist<br>新版本路径：/api/v2/pub/allNetworks<br></td><td>如果商户在进入收银台前获取了支持的网络，请进行更新</td></tr><tr><td></td><td>获取支持的币种</td><td>由原路径：api/v1/public/cryptocurrencies<br>新版本路径：/api/v2/pub/symbolList<br></td><td>如果商户在进入收银台前获取了支持的币种，请进行更新</td></tr><tr><td></td><td>获取收款合约地址</td><td>原接口：/api/v1/contract/payment<br>新接口：/api/v2/pub/cashier/info<br></td><td>原独立获取收款地址，变更为通过收银台获取配置的合约地址信息</td></tr><tr><td></td><td>查询收款订单</td><td>原接口：<br>/api/v1/payment/qrCodePayment<br>/api/v1/payment/contractPayment<br>新接口：/order/api/v2/payorder/detail<br><br><br></td><td>如果商户主动查询了收款订单状态，请变更新的api接口</td></tr><tr><td></td><td>查询付款订单</td><td>原接口：<br>/api/v1/payout/get<br>新接口：<br>/api/v2/payout/detail<br></td><td>如果商户主动查询了付款订单状态，请变更新的api接口</td></tr></tbody></table>



***

### 附录：字段变更对照（Webhook示例）

| 旧字段      | 新字段         | 类型     | 说明          |
| -------- | ----------- | ------ | ----------- |
| `status` | `tx_status` | string | 新增交易状态细分枚举值 |
| -        | `chain_id`  | string | 新增区块链网络标识   |
