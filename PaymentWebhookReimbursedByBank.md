###### [Webhook](README.md) > [Payment webhook](PaymentWebhook.md) > Payment webhook Reimburserd by bank.

# Payment webhook Reimburserd by bank
This event is derived from a `Payment Cancelled` event. It states, that the money that earlier where transferred as
a payment, now has been transferred back to the sending party.

## POST Json payload

```JJavascript
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
| Amount           | decimal | The amount of the reimbursement.                                                        |
| PaymentType      | string  | The payment type, "BS", "LS", "DanKort", "Visa", "MasterCard", "MobilePaySubscriptions" |
| PaymentReference | string  | The payment reference, if any                                                           |
| AgreementId      | string  | The agreement id, if any                                                                |


## Valid events for ``ReimbursedByBank``

The direct-debit payment options have similar behaviour, as they can handle a cancellation before or after the 
transaction has been executed. 

| Paymnet Type | Event            | TransCodes      | Description                                                                                       |
|--------------|------------------|-----------------|---------------------------------------------------------------------------------------------------|
| BS           | ReimbursedByBank | `239`           | Bank initiated, where money are transferred from the merchant, back to the debtor.                |
| BS           | Rejected         | `237`           | No amount is available, the payment has been cancelled prior to the money transfer.               |
| BS           | ReimbursedByBank | `237` w. amount | Amount is implicated, and transferred from the merchant, back to the debtor.                      |
| LS           | Reimbursed       | `555`           | Bank initiated, where money are transferred from the merchant, back to the debtor.                |
| LS           | Rejected         | `530` w. amount | Customer initiated - Amount is implicated, and transferred from the merchant, back to the debtor. |


