---
icon: plug-circle-plus
---

# Payment Event

When changes occur to a payment order, BlockATM will send notifications via the Webhook Payment event. The included statuses are:

* When the payment order has reached the required number of on-chain confirmations.
* When the payment order has been confirmed as successfully paid.
* When the customer's order has timed out due to incomplete payment.
* When the customer cancels the payment order.

BlockATM will send the following fields to your server via the configured Webhook URL:

| name                      | comment                                                                                                                                                                                               | example                                    |
| ------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------ |
| id                        | The order number corresponding to the blockATM platform                                                                                                                                               | 8210000374                                 |
| orderNo                   | Optional. The order number corresponding to your platform.                                                                                                                                            | O20231022                                  |
| chainId                   | ChainId is a unique identifier used in blockchain networks to distinguish a particular network。.you can find the chainId in [https://chainlist.org/](https://chainlist.org/)                          | 1                                          |
| cashierId                 | <p>The payment cashier ID for receiving funds.</p><p><br></p>                                                                                                                                         | 199                                        |
| amount                    | Actual payment amount by the customer                                                                                                                                                                 | 13.410037                                  |
| custNo                    | Optional. Your customerNo who pay the order.                                                                                                                                                          | 860021                                     |
| network                   | Network name used to describe the occurrence of this transaction order. If you want to uniquely identify the corresponding network chain, it is recommended to use the chainId. (e.g: Ethereum, TRON) | Ethereum                                   |
| symbol                    | The token identifier that the customer pays with.                                                                                                                                                     | USDT                                       |
| txId                      | The transaction hash corresponding to the order on the blockchain. You can view the transaction details on the corresponding network's block explorer.                                                | 0x....                                     |
| orderType                 | 1：Smart Contract Payment 2.QR Code Payment 3:Smart Contract Address Direct                                                                                                                            | 1                                          |
| status                    | <p>-3:Client Cannel<br>-2: Failure<br>-1: TimeOut <br>0：Processing <br>1: Wait Confirm <br>9: Success</p>                                                                                             | 9                                          |
| createTime                | The time of order creation, measured in milliseconds.                                                                                                                                                 | 1693212861016                              |
| <p></p><p>fromAddress</p> | <p>The address used to pay for this order (empty if unpaid).</p><p><br></p>                                                                                                                           | 0xa9e358E33a57E67c9B84618a52f0194C345C8e35 |
| <p></p><p>blockTime</p>   | The time the order was on the blockchain                                                                                                                                                              | 1693212861016                              |

