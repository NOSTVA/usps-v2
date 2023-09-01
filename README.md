## Product Package Description Requirements
the following fields are required for package description section to successfully register a product.
```javascript
{
  originZIPCode: "string",  //^\d{5}(?:[-\s]\d{4})?$
  destinationZIPCode: "string",  //^\d{5}(?:[-\s]\d{4})?$
  weight: "number", //weight in pounds
  length: "number", //length in inches
  width: "number", //width in inches
  height: "number", //height in inches
  mailClass: "string", // options: ["PRIORITY_MAIL", "PRIORITY_MAIL_EXPRESS", "PARCEL_SELECT", "PARCEL_SELECT_LIGHTWEIGHT"]
  processingCategory: "string", //options: ["FLATS", "MACHINABLE", "IRREGULAR", "NON_MACHINABLE"],
  rateIndicator: "string",
    /*
      rateIndicator options:
      3D - 3-Digit
      3N - 3-Digit Dimensional Rectangular
      3R - 3-Digit Dimensional Nonrectangular
      5D - 5-Digit
      BA - Basic
      BB - Mixed NDC
      BM - NDC
      C1 - Cubic Pricing Tier 1
      C2 - Cubic Pricing Tier 2
      C3 - Cubic Pricing Tier 3
      C4 - Cubic Pricing Tier 4
      C5 - Cubic Pricing Tier 5
      CP - Cubic Parcel
      CM - Connect Local Mail
      DC - NDC
      DE - SCF
      DF - 5-Digit
      DN - Dimensional Nonrectangular
      DR - Dimensional Rectangular
      E4 - Priority Mail Express Flat Rate Envelope - Post Office To Addressee
      E6 - Priority Mail Express Legal Flat Rate Envelope
      E7 - Priority Mail Express Legal Flat Rate Envelope Sunday / Holiday
      FA - Legal Flat Rate Envelope
      FB - Medium Flat Rate Box/Large Flat Rate Bag
      FE - Flat Rate Envelope
      FP - Padded Flat Rate Envelope
      FS - Small Flat Rate Box
      NP - Non-Presorted
      O1 - Full Tray Box
      O2 - Half Tray Box
      O3 - EMM Tray Box
      O4 - Flat Tub Tray Box
      O5 - Surface Transported Pallet
      O6 - Full Pallet Box
      O7 - Half Pallet Box
      OS - Oversized
      P5 - Cubic Soft Pack Tier 1
      P6 - Cubic Soft Pack Tier 2
      P7 - Cubic Soft Pack Tier 3
      P8 - Cubic Soft Pack Tier 4
      P9 - Cubic Soft Pack Tier 5
      Q6 - Cubic Soft Pack Tier 6
      Q7 - Cubic Soft Pack Tier 7
      Q8 - Cubic Soft Pack Tier 8
      Q9 - Cubic Soft Pack Tier 9
      Q0 - Cubic Soft Pack Tier 10
      PA - Priority Mail Express Single Piece
      PL - Large Flat Rate Box
      PM - Large Flat Rate Box APO/FPO/DPO
      PR - Presorted
      SB - Small Flat Rate Bag
      SN - SCF Dimensional Nonrectangular
      SP - Single Piece
      SR - SCF Dimensional Rectangular
    */
}

```

## Calculate domestic-label price for an Order:
The following route will calculate the shipping label price and return an estimated price amount to be displayed to the user in shipping page before confirming the checkout.
- request:
```code
POST api/usps/domestic-label/price

Content-Type: application/json
{
  shippingAddressId: "XXXXXXXXXX",
  productId: "XXXXXXXXXX"
}

```
- response:
> totalPrice can be used to calculate the order's total amount on checkout final stage.
```code
Content-Type: application/json
{
    "totalPrice": 5.84,
}
```



