## Seller Orders Menu: Shipping Page 
When Order's status is paid, Seller have two options: **Ship** and **Refund**.

**Ship** option should take the seller to shipping page where seller can either 
1. purchase (domestic/international shipping label).
2. add tracking number manually to order.


## 1. Purchase (domestic/international shipping label).
Seller update the order's information with the following inputs:
1. Incase of purchacing a Domestic Label.

```javascript
{
  weight: "number", //weight in pounds
  length: "number", //length in inches
  width: "number", //width in inches
  height: "number", //height in inches
  domesticMailClass: "string", // options: ["PRIORITY_MAIL", "PRIORITY_MAIL_EXPRESS", "PARCEL_SELECT", "PARCEL_SELECT_LIGHTWEIGHT"]
  internationalMailClass: "string", // options: ["FIRST-CLASS_PACKAGE_INTERNATIONAL_SERVICE", "PRIORITY_MAIL_INTERNATIONAL", "PRIORITY_MAIL_EXPRESS_INTERNATIONAL", "GLOBAL_EXPRESS_GUARANTEED"]
  processingCategory: "string", //options: ["FLATS", "MACHINABLE", "NON_MACHINABLE"],
  rateIndicator: "string",
    /*
      rateIndicator options: [DR - SP]
      DR - Dimensional Rectangular
      SP - Single Piece
    */
}

```

example: 
```json
{
    "weight": 7,
    "length": 9,
    "width": 0.25,
    "height": 6,
    "mailClass": "PRIORITY_MAIL",
    "mailClass": "PRIORITY_MAIL_INTERNATIONAL",
    "processingCategory": "MACHINABLE",
    "rateIndicator": "DR",
}
```
## Yallalive Shipping Labels API
### Calculate Domestic Label Price:
Use the following route to calculate the shipping label price for an order, It should return an estimated price amount to be displayed to the buyer in the shipping page before confirming the checkout.
- request:
```javascript
POST api/usps/domestic-label/price

Content-Type: application/json
{
  shippingAddressId: "XXXXXXXXXX",
  productId: "XXXXXXXXXX"
}

```
- response:
```javascript
Content-Type: application/json
{
    "totalPrice": 11.06
}
```

### Calculate International Label Price:
- request:
```javascript
POST api/usps/international-label/price

Content-Type: application/json
{
  shippingAddressId: "XXXXXXXXXX",
  productId: "XXXXXXXXXX"
}

```
- response:
```javascript
Content-Type: application/json
{
    "totalPrice": 14.96
}
```

---

### Create Domestic Label.
- request:
```javascript
POST api/usps/domestic-label

Content-Type: application/json
{
  orderId: "XXXXXXXXXX",
}
```
- response:
```javascript
Content-Type: application/json
{
    trackingNumber: "9205590109769900012613",
    labelAddress: {
        streetAddress: "STE 150",
        secondaryAddress: "1100 WYOMING ST",
        city: "SAINT LOUIS",
        state: "MO",
        ZIPCode: "63118",
        ZIPPlus4: "2628",
        firstName: "JOE",
        lastName: "DOE",
        ignoreBadAddress: false
    },
    routingInformation: "420631182628",
    postage: 7.64,
    extraServices: [
        {
            name: "USPS Tracking",
            price: 0
        }
    ],
    zone: "01",
    commitment: {
        name: "1 Days",
        scheduleDeliveryDate: "2023-05-27"
    },
    weightUOM: "LB",
    weight: 0.5,
    fees: [],
    SKU: "DPXX0XXXXC01005"
}

Content-Type: application/pdf
File Name: label.pdf
Content-Encoding: gzip
Content-Transfer-Encoding: encode
{file data}
```

### Create Returns Domestic Label.
- request:
```javascript
POST api/usps/return-label

Content-Type: application/json
{
  orderId: "XXXXXXXXXX",
}
```
- response: same as previous.

### Cancel Domestic Label.
- request:
```javascript
DELETE api/usps/domestic-label/{trackingNumber}
```
- response: operation successful

---

### Track both Domestic and International label
- request:
```javascript
GET api/usps/tracking/{trackingNumber}
```
- response:
```javascript
{
    TrackResults: {
        RequestSeqNumber: null,
        TrackInfo: {
            @ID: "XXXXXXXXXXXXXXXXXXXX",
            TrackSummary: "USPS is now in possession of your item as of 7:31 am on February 15, 2023 in RICHMOND, VA 23227."
        }
    }
}
```

