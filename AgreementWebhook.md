###### [Webhook](README.md) > Agreement webhook

# Agreement webhook
The order webhook is executed from the FarPay' core, when the agreements are created from the payment system providers, such as Card vendors, NETS or MobilePay.

# Agreement Events
Here is the list of potential agreement events. Some of the events only apply to specific agreements. 

| Event          | Numeric Value  | Description  | MP | BS | LS | Card |
|----------------|----------------|--------------|----|----|----|------|
| Create |  100  | When the agreement is received from the provider as valid | ✅ | ✅ | ✅ | ✅ |
| Change |  110  | Changes, like changing an account number, or a card also occur when the provider returns with a result | ⛔ | ✅ | ✅ | ⛔ |
| Cancel | 120 | An agreement is cancelled instantly, and afterwards the agreement cannot be used as a payment mean. Further more, when the agreement status is provisioned to NETS, the pending payments in NETS will transision to its next state _*(*1)*_ | ✅ | ✅ | ✅ | ✅ |
| Delete | 130 | Agreement can be deleted, when never used. Otherwise it can be cancelled | ✅ | ✅ | ✅ | ✅ |

_*(*1)*_
When a BS agreement is cancelled, the pending payments will transision according to the ruleset of BS Total or BS Basic configuraiton. See the transision in the table below.

| Type      | Transision |
|-----------|------------|
| BS Total  | The payment transisions to being a payment slip, and is anotated with a new *+71 key*. And when the payment slip is paid, FarPay will be able to associate the payment with the given customer, and not with the payment. |
| BS Basic  | The payment is parked, no further processing will be made |

# Data layout
The data has a partial view of the agreement, due to security. Card information is distributed with an expiredate, and a partial masked cardnumber. Bank account information is not distributed on webhooks.

There are three ways of receiving the webhooks to your business domain.
* POST with JSON payload
* POST with XML payload
* GET with Url parametres

## POST Json payload
```JavaScript
"Agreement": {  
  "CustomerNumber" : "ABC123",  
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

###### [Webhook](README.md) > Agreement webhook
