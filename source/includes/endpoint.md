
# API Endpoint

## Development and Production Endpoint

We provide 2 API endpoints using in seperated environment.

If you are developing (or testing) please use development endpoint.

Environment | Endpoint
---------  | -----------
Development | [https://api.staging.takemetour.com/partner](https://api.staging.takemetour.com/partner)
Production | [https://api.takemetour.com/partner](https://api.takemetour.com/partner)

## Endpoint list

Path | Method | Description
---------  | ----------- | ------------
/auth/login | POST | [Login partner account](#login)
/auth/logout | DELETE | [Logout partner account](#logout)
/auth/me | GET | [Get partner account info](#user-info)
/products | GET | [Get All Products](#get-all-products)
/products/:slug | GET | [Get Product Detail](#get-product-detail)
/products/price | POST | [Get Product Price](#get-product-price)
/calendar | GET | [Get Product availability](#availability)
/book | POST | [Book product (a.k.a. create transaction)](#book-product)
/transactions | GET | [Get All Transactions](#get-all-transactions)
/transactions/:id | GET | [Get Transaction detail](#transaction-detail)
/transactions/:id/voucher | GET | [Get Transaction voucher](#voucher)
