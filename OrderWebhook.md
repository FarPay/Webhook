# Order webhook
The order webhook is executed from the FarPay' PaymentWindow, when the user commits data into the form.

# Order events
The events that are sent as webhooks are 

| Event          | Value  | Description  |
|----------------|--------|--------------|
| New            |  100  | When the request is created from the API |
| PendingPayment |  200  | In a scenario, where the user has commitied the agreement infomration e.g. direct debit with Leverandørservice or Betalingsservice, and is about to enter the initial payment into the card form or pay by MobilePay |
| PendingCustomerNumber | 300 | Pending customer number occurs after the ser has input both the agreement details of the recurring payment, as well as the initial payment if present. The system leaps to this state, when the order was created without the customer present |


# Data layout
The data focus on a complete picture of an order, including the changing status. Remark that the user input details are saved in various secured environments e.g. a PCI DSS environment for card information. These details are not carried back with the webhooks.

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

