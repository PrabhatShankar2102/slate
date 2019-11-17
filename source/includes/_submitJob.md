# Submit a Job

> To authorize, use this code:

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
```

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here"
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
```

> Make sure to replace `meowmeowmeow` with your API key.

Submits a job to the system for processing, bypassing the customers cart.

### POST /jobs/{id}/submit

Submitting a job requires POSTing a request to:

`
https://{username}:{password}@rest.click2mail.com/molpro/jobs/{id}/submit
/billingType = “Credit Card”
/billingName = “John Smith”
/billingCompany = “Click2Mail”
/billingAddress1 = “3102 10th St N”
/billingAddress2 = “Suite 201”
/billingCity = “Arlington”
/billingState = “Va”
/billingZip = “22201”
/billingCountry = “USA”
/billingCcType = “VI”
/billingNumber  = “4111111111111111”
/billingMonth = “12”
/billingYear = “16”
/billingCvv = “123”
`

<aside class="notice">
You must replace <code>username</code> and <code>password</code>with your credentials.
</aside>

### URL Parameters

Parameter | Type | Description
--------- | ----------- | -----------
shipName	| Optional |	Shipping address Name
shipOrganization	| Optional |	Shipping address Organization
shipAddress1	| Optional |	Shipping address line 1
shipaddress2	| Optional |	Shipping address line 2
shipCity	| Optional |	Ship address City
shipState	| Optional |	Ship address State
shipZip	| Optional |	Ship address Zip Code
shipCountry	| Optional |	Leave blank for USA
shipperName	| Optional |	Shipper
shipMethod	| Optional |	Shipping Method
billingType	| Required | Payment Method
billingName	| Required (Credit Card only) | Name as on the card
billingCompany	| Optional |	Company
billingAddress1	| Required (Credit Card only) | Street address line 1
billingAddress2	| Optional | (Credit Card only) | Street address line 2
billingAddress3	| Optional | (Credit Card only) | Street address line 3
billingCity	| Required (Credit Card only) | City
billingState	| Required (Credit Card only) | State
billingZip	| Required (Credit Card only) | ZIP code
billingCountry	| Optional |	Required for non USA addresses
billingCcType	| Required (Credit Card only) |	Credit card type
billingNumber	| Required (Credit Card only) | Credit card number
billingMonth	| Required (Credit Card only) | Expiration month, 2 digits
billingYear	| Required (Credit Card only) | Expiration year, 2 digits
billingCvv	| Required (Credit Card only) | Credit card verification code, 3 digits
couponCode	| Optional | Coupon Code for order

Note: For Print and ship products if you do not specify a shipping address the product will be shipped to the default return address in your account. You must specify a shipper and a shipping method.

Note: To determine the possible shipping methods for your order you should use the GET /jobs/{id}/shipEstimate method.

Type |
------ |
United States Postal Service
Federal Express
United Parcel Service

Possible billing types

Type|
------ |
Credit Card
Invoice
ACH
User Credit

Possible values for billingCcType

Status | Description |
------ | -----
AE  | American Express
DI | Discover Card
MC | MasterCard
VI | Visa Card

The response will be the job submission status. You will receive XML that looks like this:

`xml
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<job>
    <id>70103</id>
    <status>0</status>
    <description>Success</description>
    <cost>1.53</cost>
    <standardCost>
        <postageName>null</postageName>
        <postageUnitCost>0.0</postageUnitCost>
        <quantity>0</quantity>
        <handlingFee>0.0</handlingFee>
        <subtotal>0.0</subtotal>
    </standardCost>
    <nonstandardCost>
        <postageName>null</postageName>
        <postageUnitCost>0.0</postageUnitCost>
        <quantity>0</quantity>
        <handlingFee>0.0</handlingFee>
        <subtotal>0.0</subtotal>
    </nonstandardCost>
    <internationalCost>
        <postageName>First Class International Letter</postageName>
        <postageUnitCost>1.15</postageUnitCost>
        <quantity>1</quantity>
        <handlingFee>0.0</handlingFee>
        <subtotal>1.15</subtotal>
    </internationalCost>
    <productionCost>
        <productionUnitCost>0.38</productionUnitCost>
        <quantity>1</quantity>
        <discountSubtotal>0.0</discountSubtotal>
        <subtotal>0.38</subtotal>
    </productionCost>
    <statusUrl>https://dev-rest.click2mail.com/molpro/jobs/70103</statusUrl>
</job>
`

### Possible return status

Status | Description
------- | ---------
0 |	Created
1 |	Job ID was not found
2 |	Payment was not authorized
9 |	Error in Job Submission
9 | Coupon code has been used before. You are not allowed to use the coupon more than xx.
9 | Coupon code has exceeded total number of uses. The total number of uses for this coupon is xx
9 |	Coupon code has expired. Expiration date is {date}.
