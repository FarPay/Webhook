# Welcome
FarPay has extended the event model with external webhooks, that are fire internal events to your invoice/payment system.

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
