###### [Webhook](README.md) > [Payment webhook](PaymentWebhook.md) > Payment webhook Rejected.

# Payment webhook rejected
The customer has rejected a schedule payment. This can be done by cancelling in the customer online bank e.g. when cancelling an BS payment.

## POST Json payload

```JavaScript
{
    "Type": "Payment",
    "Event": "RejectedByCustomer",
    "InvoiceNumber": "12345678abcnnn",
    "CustomerNumber": "abc123",
    "PaymentDueDate": "yyyy-mm-dd, // Rejected
    "Currency": "DKK", // Currency
    "InvoiceAmount": "123.1234", // Original amount
    "Amount": "123.1234", // Refunded amount
    "PaymentType": "BS", // BS, LS, DanKort, Visa, MasterCard, MobilePaySubscriptions
    "PaymentReference": "",
    "AgreementId": ""
}
```

# Values in the payload
When the different payment types are executed in this context, the values have different behaviour, due to the different features of the payment technology.

| Type               | Behaviour                   | Reason                |
|--------------------|-----------------------------|-----------------------|
| BS                 | The Amount is 0 (zero)      | The money has not been transfer from the debtors account to yours in the originated payment - Hence no payment is refunded |
| MobilePay          | InvoiceAmount and Amount can be different | When the amount is provisioined from MobilePay, it can differe from the originated amount |
| 

# Example values

BS Rejection, prior to the payment in the bank. If the payment has occur, and the customer rejects the payment (within the 10th day after the paymentdate, the amount will be present). Partial cancel is not possible as BS only deals with full cancel of the payment.

```JavaScript
{
    "Type": "Payment",
    "Event": "RejectedByCustomer",
    "InvoiceNumber": "234-cvcv-445673",
    "CustomerNumber": "123123123123",
    "PaymentDueDate": "2022-07-01",
    "Currency": "DKK",
    "InvoiceAmount": "750.9900",
    "Amount": "0.0000",
    "PaymentType": "BS",
    "PaymentReference": "",
    "AgreementId": ""
}
```

MobilePay subscriptions rejection, with a different refunded amount. This is only mentioned as an optional feature, as the payments often are the same.

```JavaScript
{
    "Type": "Payment",
    "Event": "RejectedByCustomer",
    "InvoiceNumber": "61652886",
    "CustomerNumber": "3209659",
    "PaymentDueDate": "2022-06-30",
    "Currency": "DKK",
    "InvoiceAmount": "1990.0000",
    "Amount": "1589.1800",
    "PaymentType": "MobilePaySubscriptions",
    "PaymentReference": "",
    "AgreementId": ""
}

```
