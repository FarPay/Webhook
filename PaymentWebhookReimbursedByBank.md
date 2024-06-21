###### [Webhook](README.md) > [Payment webhook](PaymentWebhook.md) > Payment webhook Reimburserd by bank.

# Payment webhook Reimburserd by bank
This event is derived from a `Payment Cancelled` event. This event specifies, that the money have been transferred, to 
the receiving party, but is now returned to the originated account.
The characteristic of this event, over the regular `Payment Cancelled`, is that money are transferred back and forth. 
This behaviour is unique for this callback-event.

## POST Json payload

```JSON
{
    "Type": "Payment",
    "Event": "ReimbursedByBank",
    "InvoiceNumber": "234-cvcv-445673",
    "CustomerNumber": "123123123123",
    "PaymentDueDate": "yyyy-mm-dd",
    "Currency": "DKK", // Currency
    "InvoiceAmount": "750.9900", // Original amount
    "Amount": "750.9900", // Reimbursed amount
    "PaymentType": "BS",  // BS, LS, DanKort, Visa, MasterCard, MobilePaySubscriptions
    "PaymentReference": "",
    "AgreementId": "12345"
}
```
## Dictionary
| Name             | Type    | Description                                                                             |
|------------------|---------|-----------------------------------------------------------------------------------------|
| Type             | string  | Always "Payment"                                                                        |
| Event            | string  | Always "ReimbursedByBank"                                                               |
| InvoiceNumber    | string  | The invoice number ```[a-zA-Z0-9](15)```                                                |
| CustomerNumber   | string  | The customer number ```[a-zA-Z0-9](15)```                                               |
| Currency         | string  | The currency of the payment, "DKK", "EUR"                                               |
| InvoiceAmount    | decimal | The original amount of the invoice                                                      |
| Amount           | decimal | The amount of the payment                                                               |
| PaymentType      | string  | The payment type, "BS", "LS", "DanKort", "Visa", "MasterCard", "MobilePaySubscriptions" |
| PaymentReference | string  | The payment reference, if any                                                           |
| AgreementId      | string  | The agreement id, if any                                                                |

## Valid events for ``ReimbursedByBank``

| Paymnet Type | Event        | Description                                                                       |
|--------------|--------------|-----------------------------------------------------------------------------------|
| BS           | Reimbursment | Bank initiated, where money are transferred from the merchant, back to the debtor |

When reimbusment is a part of BS and LS, where the money are transferred back to the debtor. 

