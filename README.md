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



