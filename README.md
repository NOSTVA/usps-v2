## Product Package Description Requirements
When creating a new product, require the seller to fill the following fields as product's package description.
```javascript
{
  weight: "number", //weight in pounds
  length: "number", //length in inches
  width: "number", //width in inches
  height: "number", //height in inches
  mailClass: "string", // options: ["PRIORITY_MAIL", "PRIORITY_MAIL_EXPRESS", "PARCEL_SELECT", "PARCEL_SELECT_LIGHTWEIGHT"]
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
    "processingCategory": "MACHINABLE",
    "rateIndicator": "DR",
}
```

## Yallalive Shipping Labels API
### Calculate domestic-label price for an Order:
The following route will calculate the shipping label price and return an estimated price amount to be displayed to the user in shipping page before confirming the checkout.
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
totalBasePrice can be used to calculate the order's total amount on checkout final stage.

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
    "trackingNumber": "9205590109769900012613",
    "labelAddress": {
        "streetAddress": "STE 150",
        "secondaryAddress": "1100 WYOMING ST",
        "city": "SAINT LOUIS",
        "state": "MO",
        "ZIPCode": "63118",
        "ZIPPlus4": "2628",
        "firstName": "JOE",
        "lastName": "DOE",
        "ignoreBadAddress": false
    },
    "routingInformation": "420631182628",
    "postage": 7.64,
    "extraServices": [
        {
            "name": "USPS Tracking",
            "price": 0
        }
    ],
    "zone": "01",
    "commitment": {
        "name": "1 Days",
        "scheduleDeliveryDate": "2023-05-27"
    },
    "weightUOM": "LB",
    "weight": 0.5,
    "fees": [],
    "SKU": "DPXX0XXXXC01005"
}

Content-Type: application/pdf
File Name: label.pdf
Content-Encoding: gzip
Content-Transfer-Encoding: encode

{file data}
```


