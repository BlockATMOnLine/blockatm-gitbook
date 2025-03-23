---
icon: cubes
---

# Payment Event

When changes occur to a payment order, BlockATM will send notifications via the Webhook Payment event. The included statuses are:

* When the payment order has reached the required number of on-chain confirmations.
* When the payment order has been confirmed as successfully paid.
* When the customer's order has timed out due to incomplete payment.
* When the customer cancels the payment order.

BlockATM will send the following fields to your server via the configured Webhook URL:

| name        | comment                                                                                                                                                                                               | example       |
| ----------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------- |
| amount      | Actual payment amount by the customer                                                                                                                                                                 | 13.410037     |
| chainId     | ChainId is a unique identifier used in blockchain networks to distinguish a particular network。.you can find the chainId in [https://chainlist.org/](https://chainlist.org/)                          | 1             |
| custNo      | Optional. Your customerNo who pay the order.                                                                                                                                                          | 860021        |
| orderNo     | Optional. The order number corresponding to your platform. This value is null when the type is 3.                                                                                                     | O20231022     |
| fee         | The order fee.The unit is USDT.                                                                                                                                                                       | 2             |
| network     | Network name used to describe the occurrence of this transaction order. If you want to uniquely identify the corresponding network chain, it is recommended to use the chainId. (e.g: Ethereum, TRON) | Ethereum      |
| platOrderNo | The order number corresponding to the blockATM platform                                                                                                                                               | 8210000374    |
| symbol      | The token identifier that the customer pays with.                                                                                                                                                     | USDT          |
| txId        | The transaction hash corresponding to the order on the blockchain. You can view the transaction details on the corresponding network's block explorer.                                                | 0x....        |
| type        | 1：Smart Contract Payment 2.QR Code Payment 3:Smart Contract Address Direct                                                                                                                            | 1             |
| status      | -1: Failure: 0：Processing 1:Success                                                                                                                                                                   | 1             |
| createTime  | The time of order creation, measured in milliseconds.                                                                                                                                                 | 1693212861016 |
