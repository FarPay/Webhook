# Agreement webhook
The order webhook is executed from the FarPay' core, when the agreements are created from the payment system providers, such as Card vendors, NETS or MobilePay.

# Agreement Events
The events that are sent as webhooks are 

| Event          | Value  | Description  |
|----------------|--------|--------------|
| Agreement Created |  100  | When the agreement is received from the provider as valid |
| Agreement Changed |  110  | Changes, like changing an account number, or a card also occur when the provider returns with a result |
| Agreement Deleted | 120 | An agreement is deleted instantly, and afterwards the agreement cannot be used as a payment mean |


# Data layout
The data has a partial view of the agreement, due to security. Card information is distributed with an expiredate, and a partial masked cardnumber. Bank account information is not distributed on webhooks.

There are three ways of receiving the webhooks to your business domain.
* POST with JSON payload
* POST with XML payload
* GET with Url parametres

## POST Json payload
```JavaScript
"Agreement": {  
  "CustomerNumber" : "2",  
  "AgreementId" : "12345",
  "AgreementType" : "Card", 
  "CardMask" : "1234 XXXXX XXXXX 4321",
  "CardExpire" : "202009",
  "Event" : "Create"
  }
```

## POST XML payload

```XML
<Agreement>
  <CustomerNumber>2</CustomerNumber>
  <AgreementId>12345</AgreementId>
  <ExternalId>REF99102933C</ExternalId>
  <AgreementType>Card</AgreementType>
  <CardMask>1234 XXXX XXXX 4321</CardMask>
  <CardExpire>202009</CardExpire>
  <Event>Create</Event>
</Order>
```

## GET url parameters

```
https://<yourdomain>/SomeEndpoint/?CustomerNumber=2&AgreementId=12345&AgreementType=CardMask&Created=1234 XXXX XXXX 4321&CardExpire=202009&Event=Create
```

