---
icon: arrows-to-circle
---

# Migration

## 新版版本升级指南（V2）

**目标**：帮助商户快速定位改动点，减少接入成本。



<table><thead><tr><th>功能模块</th><th>变更类型</th><th width="296.4847412109375">具体调整内容</th><th>商户应对措施</th><th>优先级</th><th>兼容性说明</th></tr></thead><tbody><tr><td><strong>连钱包支付</strong></td><td>参数校验增强</td><td>1. <code>custno</code> 字段改为必填<br>2. URL参数签名从可选调整为强制（使用HMAC-SHA256）</td><td>1. 检查代码是否传递<code>custno</code><br>2. 集成签名逻辑（参考签名文档）</td><td>高</td><td>旧版API停用时间：2024-12-01</td></tr><tr><td><strong>二维码支付</strong></td><td>对接方式重构</td><td>从API生单改为Widget集成（需前端嵌入）</td><td>1. 移除原有API调用<br>2. 集成新Widget（<a href="../cashier/widget-start.md">参考Widget集成指南</a>）</td><td>高</td><td>旧版立即停用</td></tr><tr><td><strong>付款功能</strong></td><td>功能扩展</td><td>新增API接口：<code>POST /v2/payout/create</code><br>（支持JSON请求，替代部分Excel场景）</td><td>1. 可选迁移至API（推荐）<br>2. 仍支持Excel上传（但功能受限）</td><td>中</td><td>新旧方式并行</td></tr><tr><td><strong>Webhook</strong></td><td>算法与字段调整</td><td>1. 签名算法改为RSA-SHA256<br>2. 新增状态字段：<code>tx_status</code>（替换原<code>status</code>）</td><td>1. 更新验签逻辑<br>2. 适配新字段（字段映射表）</td><td>高</td><td>旧版Webhook保留30天</td></tr><tr><td><strong>API接口</strong></td><td>全局升级</td><td>1. 路径前缀改为<code>/v2/</code><br>2. 签名方式统一为OAuth2.0</td><td>1. 修改请求路径<br>2. 申请OAuth2.0密钥（联系技术支持）</td><td>强制</td><td>旧版API停用时间：2024-12-01</td></tr></tbody></table>







***

### 附录：字段变更对照（Webhook示例）

| 旧字段      | 新字段         | 类型     | 说明          |
| -------- | ----------- | ------ | ----------- |
| `status` | `tx_status` | string | 新增交易状态细分枚举值 |
| -        | `chain_id`  | string | 新增区块链网络标识   |
