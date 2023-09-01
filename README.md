## Product Package Description Requirements
When creating a new product, require the seller to fill the following fields as product's package description.
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
totalBasePrice can be used to calculate the order's total amount on checkout final stage.
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
    "totalBasePrice": 11.06
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
    "totalBasePrice": 14.96
}
```

---

### Create domestic-label.
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


