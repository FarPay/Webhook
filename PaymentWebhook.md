###### [Webhook](README.md) > Payment webhook

# Payment webhook
The payment webhook is executed from the FarPay' core system, since it exposes events that occur between FarPay and the payment service provider, e.g. Card provider, MobilePay or NETS.

# Payment events
The events that are sent as webhooks are 

| OrderEvent     | Value  | Description  |
|----------------|--------|--------------|
| Succeeded      |  200   | The payment was successfully executed |
| Canceled       |  210   | The customer has cancelled the payment |
| Failed         |  220   | The paiment failed, e.g. beause lack of funds, card has expired, a negative outcome of the attempt of paying an amount |
| RejectedByCustomer | 230 | The customer has rejected a schedule payment. This can be done by cancelling in the customer online bank |
| ReimbursedByBank | 240 |  The financial institution of the customer is cancelling the payment. A typical scenario is that the customer does not have sufficient funds, or might have passed. |

# Payment Type
The given payment type is also specified in the webhook event, the available types are

| Type                   | Description                                  |
|------------------------|----------------------------------------------|
| BS                     | Betalingsservice                             |
| LS                     | Leverandørservice                            |
| FI                     | FI-Indbetalingskort (+71)....                |
| DanKort                | Dankort                                      |
| Visa                   | Visa                                         |
| MasterCard             | MasterCard                                   |
| MobilePaySubscriptions | MobilePay Subscriptions (Recurring Payments) |
| MobilePayInvoice       | MobilePay Invoice (Single payments)          |


# Data layout
The data is focused on giving the information of what is paid, the amount and how it was paid.

There are three ways of receiving the webhooks to your business domain.
* POST with JSON payload
* POST with XML payload
* GET with Url parametres



## POST Json payload
```JavaScript
{  
  "Event" : "Succeeded",
  "PaymentReference" : "ABC123-Reference",
  "InvoiceNumber": "1234567BAVV",
  "CustomerNumber" : "66776655",
  "PaymentDueDate" : "2018-05-02",
  "Currency": "DKK",
  "InvoiceAmount" : 120.25,
  "Amount" : 90.95,
  "PaymentType" : "BS"
}
```

## POST XML payload

```XML
<Payment>
  <Event>Succeeded</Event>
  <PaymentReference>ABC123-Reference</PaymentReference>
  <InvoiceNumber>1234567BAVV</InvoiceNumber>
  <CustomerNumber>66776655</CustomerNumber>
  <PaymentDueDate>2018-05-02</PaymentDueDate>
  <Currency>DKK</Currency>
  <InvoiceAmount>120.25</InvoiceAmount>
  <Amount>90.95</Amount>
  <PaymentType>BS</PaymentType>
</Payment>
```

## GET url parameters

```
https://<yourdomain>/SomeEndpoint/?Event=Succeeded&PaymentReference=ABC123-Reference&InvoiceNumber=1234567BAVV&CustomerNumber=66776655&PaymentDueDate=2018-05-02&Currency=DKK&InvoiceAmount=120.25&Amount=90.95&PaymentType=BS
```

###### [Webhook](README.md) > Payment webhook
