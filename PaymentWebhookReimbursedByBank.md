###### [Webhook](README.md) > [Payment webhook](PaymentWebhook.md) > Payment webhook Reimburserd by bank.

# Payment webhook Reimburserd by bank
The financial institution of the customer is cancelling the payment. A typical scenario is that the customer does not have sufficient funds, or might have passed.

## POST Json payload

```JavaScript
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
    "AgreementId": ""
}
```

