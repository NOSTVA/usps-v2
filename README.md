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

## Calculate domestic-label price for an Order:
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
> totalBasePrice can be used to calculate the order's total amount on checkout final stage.
```code
Content-Type: application/json
{
    "totalBasePrice": 11.06,
    "rates": [
        {
            "SKU": "DUXP0XXXXC05070",
            "description": "USPS Ground Advantage Nonmachinable Single-piece",
            "priceType": "COMMERCIAL",
            "price": 11.06,
            "weight": 7,
            "dimWeight": 0,
            "fees": [],
            "startDate": "2023-07-09",
            "endDate": "",
            "warnings": [],
            "mailClass": "USPS_GROUND_ADVANTAGE",
            "zone": "05"
        }
    ]
}
```



