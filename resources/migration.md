---
description: 新版版本升级指南（V2）
icon: arrows-to-circle
---

# Migration

**目标**：帮助商户快速定位改动点，减少接入成本。







<table><thead><tr><th width="105.78790283203125">功能模块</th><th>旧版本</th><th>新版本</th><th>商户应对措施</th></tr></thead><tbody><tr><td><strong>连钱包支付</strong></td><td>通过widget 接入收银台<br>1. 客户编号custno 选填<br>2. URL参数签名选填（签名方式为ECDSA）</td><td><br>通过widget接入收银台<br>1. <code>custno</code> 字段改为必填<br>2. URL参数签名从可选调整为强制（使用HMAC-SHA256）<br></td><td>1.<a href="../quick-start/deposit-service.md">充值接入流程</a><br>1. 检查代码是否传递custNo<br>2. 集成签名逻辑（参考<br><a href="../cashier/can-shu-qian-ming.md">签名文档</a>下方签名方式变更附录二）</td></tr><tr><td><strong>二维码支付</strong></td><td>通过api创建订单，并且返回收银台地址</td><td>通过widget方式接入收银台</td><td>1. 移除原有API调用，参考新的<a href="../quick-start/deposit-service.md">充值接入流程</a><br>2. 集成新Widget（参考<br><a href="../cashier/widget-start.md">Widget集成指南</a>）<br></td></tr><tr><td><strong>付款功能</strong></td><td>1.在商户端上传付款订单</td><td><ol><li>保留在商户端上传付</li><li>增加通过api创建付款订单 </li></ol></td><td><ol><li>选择通过<a href="../open-api/payout-data/create-payout-order.md">创建付款订单API</a>接入<br></li></ol></td></tr><tr><td><strong>Webhook</strong></td><td><p></p><ol><li>签名算法为ECDSA<br></li><li>订单状态status为int</li></ol><p></p></td><td><ol><li>签名算法调整为<br>HMAC-SHA256</li><li>订单状态status 为String </li></ol></td><td><p>签名字符串逻辑未变更 </p><p>1.更新验签逻辑 （参考<a href="../webhook/signing.md">签名文档</a>）<br>2. 适配新字段（<br>具体见下方 附录一）</p></td></tr><tr><td><strong>API接口</strong></td><td>路径为/api/v1</td><td><br>路径升级为/api/v2<br></td><td>详情见 附录三 api 变更</td></tr><tr><td></td><td>获取支持的网络</td><td>由原路径：/api/v1/public/networklist<br>新版本路径：/api/v2/pub/allNetworks<br></td><td>如果商户在进入收银台前获取了支持的网络，请进行更新</td></tr><tr><td></td><td>获取支持的币种</td><td>由原路径：api/v1/public/cryptocurrencies<br>新版本路径：/api/v2/pub/symbolList<br></td><td>如果商户在进入收银台前获取了支持的币种，请进行更新</td></tr><tr><td></td><td>获取收款合约地址</td><td>原接口：/api/v1/contract/payment<br>新接口：/api/v2/pub/cashier/info<br></td><td>原独立获取收款地址，变更为通过收银台获取配置的合约地址信息</td></tr><tr><td></td><td>查询收款订单</td><td>原接口：<br>/api/v1/payment/qrCodePayment<br>/api/v1/payment/contractPayment<br>新接口：/order/api/v2/payorder/detail<br><br><br></td><td>如果商户主动查询了收款订单状态，请变更新的api接口</td></tr><tr><td></td><td>查询付款订单</td><td>原接口：<br>/api/v1/payout/get<br>新接口：<br>/api/v2/payout/detail<br></td><td>如果商户主动查询了付款订单状态，请变更新的api接口</td></tr></tbody></table>

###



***

### 附录一：字段变更对照（Webhook 收款）

| 旧字段         | 新字段       | 类型     | 说明                                                                 |
| ----------- | --------- | ------ | ------------------------------------------------------------------ |
| platOrderNo | `id`      | long   | BlockATM唯一订单标识                                                     |
| type        | orderType | int    | 收款订单类型                                                             |
| status      | status    | String | <p>由数字变更为字符串：<br>CANCELLED EXPIRED</p><p>PENDING</p><p>SUCCESS</p> |
| -           | blockTime | long   | 新增字段，返回交易所在区块链上创建时间                                                |



### 附录二：签名方式变更对照

| 配置项        | 旧版本                               | 新版本         | 说明                     |
| ---------- | --------------------------------- | ----------- | ---------------------- |
| 对接公钥       | 【智能合约支付】/【二维码支付】->【设定】-【API】      | 【收银台】-【对接】  | 集成widget收银台参数、api签名请求头 |
| 对接密钥       | 【智能合约支付】/【二维码支付】->【设定】-【API】      | 【收银台】-【对接】  | 收银台参数，api参数签名密钥        |
| webhook密钥  | 【智能合约支付】/【二维码支付】->【设定】->【webhook】 | 【收银台】-【对接】  | webhook验签密钥            |
| webhook 地址 | 【智能合约支付】/【二维码支付】->【设定】->【webhook】 | 【收银台】-【对接】  | webhook 通知地址           |
| 签名规则       | 按字符&连接排序                          | 按字符&连接排序    | 签名规则未变化                |
| 签名算法       | ECDSA                             | HMAC-SHA256 |                        |





f





### 附录三（教学视频）：

1. 创建收币合约&#x20;

{% file src="../.gitbook/assets/创建收币合约.mp4" %}

2. 创建收银台&#x20;

{% file src="../.gitbook/assets/创建收银台.mp4" %}

3. 收银台对接&#x20;

{% file src="../.gitbook/assets/收银台对接.mp4" %}

