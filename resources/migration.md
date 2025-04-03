---
icon: arrows-to-circle
---

# Migration

## 新版版本升级指南（V2）

**目标**：帮助商户快速定位改动点，减少接入成本。





<table><thead><tr><th width="105.78790283203125">功能模块</th><th>变更类型</th><th>具体调整内容</th><th>商户应对措施</th></tr></thead><tbody><tr><td><strong>连钱包支付</strong></td><td>参数校验增强</td><td>1. <code>custno</code> 字段改为必填<br>2. URL参数签名从可选调整为强制（使用HMAC-SHA256）<br></td><td>1.<a href="../quick-start/deposit-service.md">充值接入流程</a><br>1. 检查代码是否传递custNo<br>2. 集成签名逻辑（参考<br><a href="../cashier/can-shu-qian-ming.md">签名文档</a>下方签名方式变更附录）</td></tr><tr><td><strong>二维码支付</strong></td><td>对接方式重构</td><td>从API生单改为Widget集成（需前端嵌入）</td><td>1. 移除原有API调用，参考新的<a href="../quick-start/deposit-service.md">充值接入流程</a><br>2. 集成新Widget（参考<br><a href="../cashier/widget-start.md">Widget集成指南</a>）<br></td></tr><tr><td><strong>付款功能</strong></td><td>功能扩展</td><td>新增API接口：<code>POST</code> /api/v2/payout/order</td><td>1.通过<a href="../open-api/payout-data/create-payout-order.md">创建付款订单API</a>接入<br>2. 仍支持商户通过Excel上传</td></tr><tr><td><strong>Webhook</strong></td><td>算法与字段调整</td><td>1. 签名方式未变更，签名算法调整为HMAC-SHA256<br>2. status 字段由int 类型调整为字符串<br></td><td>1. 更新验签逻辑 （参考<a href="../webhook/signing.md">签名文档</a>）<br>2. 适配新字段（<br>具体见下方附录）</td></tr><tr><td><strong>API接口</strong></td><td>版本升级</td><td>openApi 升级为/v2版本，部分接口逻辑调整，详情见下面列表：<br><br></td><td></td></tr><tr><td></td><td>获取支持的网络</td><td>由原路径：/api/v1/public/networklist<br>新版本路径：/api/v2/pub/allNetworks<br></td><td>如果商户在进入收银台前获取了支持的网络，请进行更新</td></tr><tr><td></td><td>获取支持的币种</td><td>由原路径：api/v1/public/cryptocurrencies<br>新版本路径：/api/v2/pub/symbolList<br></td><td>如果商户在进入收银台前获取了支持的币种，请进行更新</td></tr><tr><td></td><td>获取收款合约地址</td><td>原接口：/api/v1/contract/payment<br>新接口：/api/v2/pub/cashier/info<br></td><td>原独立获取收款地址，变更为通过收银台获取配置的合约地址信息</td></tr><tr><td></td><td>查询收款订单</td><td>原接口：<br>/api/v1/payment/qrCodePayment<br>/api/v1/payment/contractPayment<br>新接口：/order/api/v2/payorder/detail<br><br><br></td><td>如果商户主动查询了收款订单状态，请变更新的api接口</td></tr><tr><td></td><td>查询付款订单</td><td>原接口：<br>/api/v1/payout/get<br>新接口：<br>/api/v2/payout/detail<br></td><td>如果商户主动查询了付款订单状态，请变更新的api接口</td></tr></tbody></table>

###



***

### 附录：字段变更对照（Webhook 收款）

| 旧字段         | 新字段       | 类型     | 说明                                                                 |
| ----------- | --------- | ------ | ------------------------------------------------------------------ |
| platOrderNo | `id`      | long   | BlockATM唯一订单标识                                                     |
| type        | orderType | int    | 收款订单类型                                                             |
| status      | status    | String | <p>由数字变更为字符串：<br>CANCELLED EXPIRED</p><p>PENDING</p><p>SUCCESS</p> |
| -           | blockTime | long   | 新增字段，返回交易所在区块链上创建时间                                                |



### 附录：签名方式变更对照

| 配置项        | 旧版本                               | 新版本         | 说明                     |
| ---------- | --------------------------------- | ----------- | ---------------------- |
| 对接公钥       | 【智能合约支付】/【二维码支付】->【设定】-【API】      | 【收银台】-【对接】  | 集成widget收银台参数、api签名请求头 |
| 对接密钥       | 【智能合约支付】/【二维码支付】->【设定】-【API】      | 【收银台】-【对接】  | 收银台参数，api参数签名密钥        |
| webhook密钥  | 【智能合约支付】/【二维码支付】->【设定】->【webhook】 | 【收银台】-【对接】  | webhook验签密钥            |
| webhook 地址 | 【智能合约支付】/【二维码支付】->【设定】->【webhook】 | 【收银台】-【对接】  | webhook 通知地址           |
| 签名规则       | 按字符&连接排序                          | 按字符&连接排序    | 签名规则未变化                |
| 签名算法       | ECDSA                             | HMAC-SHA256 |                        |



