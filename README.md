# Welcome

FarPay has extended the event model with external webhooks, that are fire internal events to your domain system.

# Communication form

All Webhooks have the it in common taht, they can be communicated with
* Url (Standard URL in a HTTP GET with parameters)
* Xml (Embeds the data as Xml in a HTTP POST)
* Json (Embeds the data as Json in a HTTP POST)

# Webhook types

The types, have different events and purpose
The events are gathered arround 
* [Payment](PaymentWebhook.md)
* [Agreement](AgreementWebhook.md)
* [Order](OrderWebhook.md)

# Setup
There are a couple of things that need attention before receiving webhooks from FarPay. First is which webhook types you want to receive. The types are listed above — they can be selected individually, or all at once.

Second is the optional but *highly recommended* security feature: webhook signing. When you add a secret to the webhook settings, FarPay signs every JSON and XML delivery with an HMAC-SHA256 signature following the [Standard Webhooks](https://www.standardwebhooks.com) specification. The signature is sent in the `webhook-id`, `webhook-timestamp` and `webhook-signature`. Webhooks without a secret are sent unsigned.

See **[Verifying webhook signatures](WebhookSignatureVerification.md)** for the full verification guide.

