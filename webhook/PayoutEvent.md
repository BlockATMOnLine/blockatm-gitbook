---
icon: plug-circle-plus
---

# Payout Event

When a payout order is completed, BlockATM will notify you of the payout event via Webhook, allowing you to promptly retrieve the results.

The following fields will be returned:

| name                    | comment                                                                                                                                                                                               | example                                    |
| ----------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------ |
| bizOrderNo              | The order number corresponding to your platform.                                                                                                                                                      | B202505220012                              |
| amount                  | The amount to be paid to the target address.                                                                                                                                                          | 13.410037                                  |
| chainId                 | ChainId is a unique identifier used in blockchain networks to distinguish a particular network。.you can find the chainId in [https://chainlist.org/](https://chainlist.org/)                          | 1                                          |
| custNo                  | Your customerNo .                                                                                                                                                                                     | 860021                                     |
| fee                     | The order fee.The unit is USDT.                                                                                                                                                                       | 2                                          |
| <p></p><p>gasAmount</p> | Actual gas consumption.The unit is USDT.                                                                                                                                                              | 1                                          |
| <p></p><p>toAddress</p> | The destination address to which the asset is to be transferred                                                                                                                                       | 0xa9e358E33a57E67c9B84618a52f0194C345C8e35 |
| network                 | Network name used to describe the occurrence of this transaction order. If you want to uniquely identify the corresponding network chain, it is recommended to use the chainId. (e.g: Ethereum, TRON) | Ethereum                                   |
| symbol                  | The token identifier that the customer pays with.                                                                                                                                                     | USDT                                       |
| txId                    | The transaction hash corresponding to the order on the blockchain. You can view the transaction details on the corresponding network's block explorer.                                                | 0x....                                     |
| type                    | 1：Smart Contract Payment 2.QR Code Payment 3:Smart Contract Address Direct                                                                                                                            | 1                                          |
| status                  | <p> 0：Processing <br> 1: Success<br>2: Refund</p>                                                                                                                                                     | 1                                          |
| createTime              | The time of order creation, measured in milliseconds.                                                                                                                                                 | 1693212861016                              |
| contractId              | <p>The unique payout contract ID you created in the BlockATM backend.</p><p><br></p>                                                                                                                  | 200910                                     |
| <p></p><p>blockTime</p> | The time the order was on the blockchain                                                                                                                                                              | 1693212861016                              |
