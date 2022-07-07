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
| [RejectedByCustomer](PaymentWebhookRejectedByCustomer.md) | 230 | The customer has rejected a schedule payment. This can be done by cancelling in the customer online bank |
| [ReimbursedByBank](PaymentWebhookReimbursedByBank.md) | 240 |  The financial institution of the customer is cancelling the payment. A typical scenario is that the customer does not have sufficient funds, or might have passed. |

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
  "Type": "Payment",
  "Event": "Succeeded",
  "InvoiceNumber": "1234567BAVV",
  "CustomerNumber": "66776655",
  "PaymentDueDate": "{yyyy-MM-dd}",
  "Currency": "DKK",
  "InvoiceAmount": "1215.0000", // tusind og to hundrede og femten komma null kr.
  "Amount": "1125.0000", // tusind og to hundrede og femten komma null kr.
  "PaymentType": "LS",
  "PaymentReference": "ABC123-Reference",
  "AgreementId": "1234"
}

```

## POST XML payload

```XML
<Payment>
  <Type>Payment</Type>
  <Event>Succeeded</Event>
  <InvoiceNumber>1234567BAVV</InvoiceNumber>
  <CustomerNumber>66776655</CustomerNumber>
  <PaymentDueDate>{yyyy-MM-dd}</PaymentDueDate>
  <Currency>DKK</Currency>
  <InvoiceAmount>1215.0000</InvoiceAmount> /* tusind og to hundrede og femten komma null kr. */
  <Amount>1125.0000</Amount> /* tusind og to hundrede og femten komma null kr. */
  <PaymentType>LS</PaymentType>
  <PaymentReference>ABC123-Reference</PaymentReference>
  <AgreementId>1234<AgreementId>
</Payment>
```

## GET url parameters

```
https://<yourdomain>/SomeEndpoint/?Type=PaymentEvent=Succeeded&PaymentReference=ABC123-Reference&InvoiceNumber=1234567BAVV&CustomerNumber=66776655&PaymentDueDate={yyyy-MM-dd}&Currency=DKK&InvoiceAmount=1215.000&Amount=1215.000&PaymentType=LS
```



###### [Webhook](README.md) > Payment webhook
