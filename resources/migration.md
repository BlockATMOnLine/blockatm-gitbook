---
description: 新版版本升级指南（V2）
icon: arrows-to-circle
---

# Migration

**目标**：帮助商户快速定位改动点，减少接入成本。









| 功能模块       | 旧版本                                                                 | 新版本                                                                 | 商户应对措施                                                                 |
|----------------|----------------------------------------------------------------------|----------------------------------------------------------------------|------------------------------------------------------------------------------|
| **连钱包支付** | 通过widget 接入收银台<br>1. 客户编号custno 选填<br>2. URL参数签名选填（签名方式为ECDSA） | 通过widget接入收银台<br>1. `custno` 字段改为必填<br>2. URL参数签名从可选调整为强制（使用HMAC-SHA256） | 1.[充值接入流程](../quick-start/deposit-service.md)<br>1. 检查代码是否传递custNo<br>2. 集成签名逻辑（参考[签名文档](../cashier/can-shu-qian-ming.md)下方签名方式变更附录二） |
| **二维码支付** | 通过api创建订单，并且返回收银台地址                                   | 通过widget方式接入收银台                                             | 1. 移除原有API调用，参考新的[充值接入流程](../quick-start/deposit-service.md)<br>2. 集成新Widget（参考[Widget集成指南](../cashier/widget-start.md)） |
| **付款功能**   | 1.在商户端上传付款订单                                                | 1. 保留在商户端上传付<br>2. 增加通过api创建付款订单                  | 1. 选择通过[创建付款订单API](../open-api/payout-data/create-payout-order.md)接入 |
| **Webhook**    | 1. 签名算法为ECDSA<br>2. 订单状态status为int                          | 1. 签名算法调整为HMAC-SHA256<br>2. 订单状态status 为String           | 签名字符串逻辑未变更<br>1.更新验签逻辑（参考[签名文档](../webhook/signing.md)）<br>2. 适配新字段（具体见下方 附录一） |
| **API接口**    | 路径为/api/v1                                                        | 路径升级为/api/v2                                                   | 详情见 附录三 api 变更                                                      |

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





### 附录三 API 变更对照表
| API功能           | 旧版本路径/接口                                   | 新版本路径/接口                                   | 调整点                           |
|-------------------|------------------------------------------------|------------------------------------------------|-------------------------------|
| 获取支持的网络    | `/api/v1/public/networklist`                   | `/api/v2/pub/allNetworks`                      | 如果商户在进入收银台前获取了支持的网络，请进行更新     |
| 获取支持的币种    | `/api/v1/public/cryptocurrencies`              | `/api/v2/pub/symbolList`                       | 如果商户在进入收银台前获取了支持的币种，请进行更新     |
| 获取收款合约地址  | `/api/v1/contract/payment`                     | `/api/v2/pub/cashier/info`                     | 原独立获取收款地址，变更为通过收银台获取配置的合约地址信息 |
| 查询收款订单      | `/api/v1/payment/qrCodePayment`<br>`/api/v1/payment/contractPayment` | `/order/api/v2/payorder/detail`                | 如果商户主动查询了收款订单状态，请变更新的API接口    |
| 查询付款订单      | `/api/v1/payout/get`                           | `/api/v2/payout/detail`                        | 如果商户主动查询了付款订单状态，请变更新的API接口    |






### 附录四（教学视频）：

1. 创建收币合约&#x20;

{% file src="../.gitbook/assets/创建收币合约.mp4" %}

2. 创建收银台&#x20;

{% file src="../.gitbook/assets/创建收银台.mp4" %}

3. 收银台对接&#x20;

{% file src="../.gitbook/assets/收银台对接.mp4" %}

