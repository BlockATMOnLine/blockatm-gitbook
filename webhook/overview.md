---
icon: book-open
---

# Overview

Webhooks are used to receive real-time notifications about asynchronous events in the payment system. When the status of a transaction changes, BlockATM sends an HTTP POST request with event data to the Webhook URL configured in your account.\
This is particularly useful for handling events not triggered by direct API requests, such as transaction status updates.

## How Webhooks Work

### 1. Event Trigger

When a specific event occurs in your account (e.g., payment success, payout triggered), BlockATM sends an HTTP POST request to your Webhook URL.&#x20;

You can differentiate each webhook event type by the request header "BlockATM-Event". When "**BlockATM-Event**" is set to "**Payment**", it indicates that your payment contract has received a payment. When it is set to "**Payout**", it indicates that your payout contract has triggered a payment.

### 2. Event Type Identification

Each Webhook request includes a BlockATM-Event header to identify the event type. For example:

* Payment: A payment was received by the payment contract.
* Payout: A payout was triggered by the payout contract.

### 3.Data Reception

You need to configure an endpoint on your server to receive and process these events, updating your system accordingly.

## Secure your Webhook

You may validate incoming requests to ensure they are coming from a trusted source.\
Visit our webhooks signature for more information. This is a recommended best practice.

## Important Notes

* Ensure your Webhook URL uses HTTPS to guarantee data security.
* Your server must return an HTTP status code of 200 to confirm successful receipt of the Webhook.
* If a Webhook fails to deliver, BlockATM will retry, but it is recommended to log events for troubleshooting.
