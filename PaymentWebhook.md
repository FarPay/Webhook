# Payment webhook
The payment webhook is executed from the FarPay' core system, since it exposes events that occur between FarPay and the payment service provider, e.g. Card provider, MobilePay or NETS.

# Payment events
The events that are sent as webhooks are 

| Event          | Value  | Description  |
|----------------|--------|--------------|
| Succeeded      |  200   | The payment was successfully executed |
| Canceled       |  210   | The customer has cancelled the payment |
| Failed         |  220   | The paiment failed, e.g. beause lack of funds, card has expired, a negative outcome of the attempt of paying an amount |
| RejectedByCustomer | 230 | The customer has rejected a schedule payment. This can be done by cancelling in the customer online bank |
| ReimbursedByBank | 240 |  The financial institution of the customer is cancelling the payment. A typical scenario is that the customer does not have sufficient funds, or might have passed. |

# Data layout
The data is focused on giving the information of what is paid, the amount and how it was paid.

There are three ways of receiving the webhooks to your business domain.
* POST with JSON payload
* POST with XML payload
* GET with Url parametres

## POST Json payload
```JavaScript
"Order": {  
  "Token" : "Token123ABC",  
  "OrderEvent" : "New",
  "ExternalId" : "REF99102933C", 
  "Created" : "2018-05-02",
  "CustomerNumber" : "2" 
  }
```

## POST XML payload

```XML
<Order>
  <Token>Token123ABC</token>
  <OrderEvent>New</OrderEvent>
  <ExternalId>REF99102933C</ExternalId>
  <Created>2018-05-02</Created>
  <CustomerNumber>2</CustomerNumber>
</Order>
```

## GET url parameters

```
https://<yourdomain>/SomeEndpoint/?Token=Token123ABC&OrderEvent=New&ExternalId=REF99102933C&Created=2018-05-02&CustomerNumber=2
```

