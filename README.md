# usps-v2

## Calculate domestic-label price for an Order:
The following route will calculate the shipping label price and return an estimated price amount to be displayed to the user in shipping page before confirming the checkout.
- request:
``` 
POST api/usps/domestic-label/price
application/json
{
  shippingAddressId: "XXXXXXXXXX",
  productId: "XXXXXXXXXX"
}
```
- response:
> The totalPrice will be used to calculate the order's total amount on checkout final stage.
```
{
    "totalPrice": 5.84,
}
```



