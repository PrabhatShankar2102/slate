# Create a job

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

This function creates a new job in the customer’s account. In this function you will specify the product and mailing options, the document and list id’s and the return address if other that the default return address in your account.

There are two ways to create a job with the rest api. The first method is used when you want to specify all the job options from within the API. This method will not work when using mail merge for variable data. The second method is to use the web user interface to create a job template which is used over and over again.

### POST /jobs
Creating a job requires POSTing a request to

`https://{username}:{password}@rest.click2mail.com/molpro/jobs
/documentClass = "Letter 8.5 x 11"
/layout = "Address on Separate Page"
/productionTime = "Next Day"
/envelope = "#10 Double Window"
/color = "Black and White"
/paperType = "White 24#"
/printOption = "Printing One side"
/documentId = "12345"
/addressId = "23499734"`

<aside class="notice">
You must replace <code>username</code> and <code>password</code>with your credentials.
</aside>

### URL Parameters

Parameter | Type | Description
--------- | ----------- | -----------
documentClass | Required | The general type of the product
layout	| Required |	The specific type of the product
productionTime	| Required |	The desired production time
envelope	| Required |	If this is an enveloped product this determines the envelope in which the product is to be mailed; otherwise provide no value
color	| Required |	Print in color or black and white
paperType	| Required |	Sets the paper the mailing is to be printed on
printOption	| Required |	Sets simplex or duplex printing
documentId	| Optional|	ID of the document to print
jobDocumentID	| Optional|	document ID of the job version of the document
addressId	| Optional|	This required if the product required a recipient address list
mailClass	| Optional|	Overrides the default of First Class for mailed products
rtnName	| Optional|	Return address Name
rtnOrganization	| Optional|	Return address Organization
rtnaddress1	| Optional|	Return address line 1
rtnaddress2	| Optional|	Return address line 2
rtnCity	| Optional|	Return address City
rtnState	| Optional|	Return address State
rtnZip	| Optional|	Return address Zip Code
endorsement	| Optional|	Ancillary endorsement service, the default is none
appSignature	| Optional|	This is a short signature to identify orders that come from your app
projectId	| Optional|	use to place this job in a pre-existing project in your account
mailingDate	| Optional|	Used to schedule the mailing date in the future. Format YYYYMMDD. If not provided the order will be mailed on the next available on the next business day. The business day cut off is 8PM EST.
quantity	| Optional|	For products that do not use mailing lists. Quantity to print
returnAddressId	| Optional|	You may use the return address id to specify a return address already in your account
courtesyReplyAddressId	| Optional|	If you are mailing a courtesy reply mail product use this to specify a courtesy reply address already in your account
businessReplyAddressId	| Optional|	If you are mailing a business reply mail product use this to specify the busines reply address and permit information already in your account
enclosure	| Optional|	Identifies the special enclosure to use with this order. Special enclosures must be pre-arranged with Click2Mail


The optional application signature is used by developers who write applications that use our API and have the need for Click2mail to identify the orders generated from the application for affiliate tracking or other pre-arranged reasons. The use of this identifier is usually pre-arranged with Click2mail.

Either a base document ID or a job document id is required before you can submit the job, you cannot use both.

The XML response looks like this:

`xml
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<job>
  <id>245985>/id>
  <status>0</status>
  <description>Created</description>
  <statusUrl>https://rest.click2mail.com/molpro/jobs/245985</statusUrl>
</job>
`

### Possible return status

Status | Description
------- | ---------
0 |	Created
9 |	Document ID not found
9 |	Job Document ID not found
9 |	Address List ID not found
9 |	Document Type cannot Mail Internationally
9 |	Document Number of Pages outside range for product
9 |	Project does not exist
9 |	Invalid product options. Sku not found.
9 |	Could not parse date. Please add mailingDate parameter in form ‘yyyymmdd
9 |	Mailing date should be greater than current date.
9 |	Future date greater than 9 |0 | days.
9 |	Address list not valid for selected Product
9 |	Endorsements not valid for selected product
9 |	Return Address not valid for selected product
9 |	Minimum Quantity for selected product is xxxxx
9 |	Maximum Quantity for selected product is xxxxx
9 |	BaseDocument class doesn’t match to the class associated with this job.
9 |	JobDocument class doesn’t match to the class associated with this job.
9 |	returnAddressId not valid for selected product.
9 |	courtesyReplyAddressIdnot valid for selected product.
9 |	businessReplyAddressId valid for selected product.
9 |	returnAddressId is invalid.
9 |	courtesyReplyAddressId is invalid.
9 |	businessReplyAddressId is invalid.
9 |	Address identified by returnAddressId is not a return address.
9 |	Address identified by courtesyReplyAddressId is not a courtesy_reply address.
9 |	Address identified by businessReplyAddressId is not a business_reply address.
9 |	Enclosure {enclosure} not found for user {username}
9 |	Enclosure {enclosure} is not allowed for SKU {sku}