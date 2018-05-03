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
There are a couple of features, that needs attention before receiving any webhooks from FarPay. Firstoff is what webhook types you want to receive. The types are mentioned above - they can be selected individually, or all.

Secondly, the security enhancement which is an optional feature of the webhooks, but *highly reccomended* feature, to ensure message integrety. The step consists of adding a secret to the webhook settings, where as FarPay concatenates the value with the secret, and outputs a checksom, that is appended to the webhook payload or url.
