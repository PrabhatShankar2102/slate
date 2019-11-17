# Create an AddressList

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

This method is used to create the address list for a mailing in your account. This requires that you have created the addressMappingId as described in the [Quick Start Guide](https://dev-developers.click2mail.com/rest-api/molpro/getting-started/quick-start)

### POST /addressLists
Submitting address lists requires POSTing a request to:

`This sample uses our standard address template and mapping.
https://{username}:{password}@rest.click2mail.com/molpro/addressLists -H "Content-Type: application/xml" -d "<addressList>
  <addressListName>Best Customers</addressListName>
  <addressMappingId>2</addressMappingId>
  <addresses>
    <address>
      <First_name>John</First_name>
	  <Last_name>Smith</Last_Name>
	  <Organization>My Business</Organization>
      <Address1>123 Some Street</><Address1>
	  <Address2>Suite 210</>Address2>
	  <Address3></Address3>
      <City>Somewhere</City>
      <State>Va</State>
      <Zip>12345</Zip>
	  <Country_non-US></Country_non-US>
    </address>
	<address>
      <First_name>Mary</First_name>
	  <Last_name>Smith</Last_Name>
	  <Organization>My Business</Organization>
      <Address1>123 Some Street</><Address1>
	  <Address2>Suite 210</>Address2>
	  <Address3></Address3>
      <City>Rio de Janerio</City>
      <State>CEP</State>
      <Zip>222021 001</Zip>
	  <Country_non-US>Brazil</Country_non-US>
    </address>
  </addresses>
</addressList>"
`


`
This sample uses a custom address template and mapping that could be created in your account through our UI.
https://{username}:{password}@rest.click2mail.com/molpro/addressLists -H "Content-Type: application/xml" -d "<addressList>
  <addressListName>Best Customers</addressListName>
  <addressMappingId>123</addressMappingId>
  <addresses>
    <address>
      <name>John Smith</name>
	  <organization>My Business</organization>
      <address>123 Some Street</><address>
      <city>Somewhere</city>
      <state>Va</state>
      <postCode>12345</postCode>
	  <country></country>
    </address>
	<address>
      <name>Mary Smith</name>
	  <organization>My Business</organization>
      <address>123 Some Street</><addressa>
      <city>Rio de Janerio</city>
      <state>CEP</state>
      <postCode>222021 001</postCode>
	  <country>Brazil</country>
    </address>
  </addresses>
</addressList>"
`
<aside class="notice">
You must replace <code>username</code> and <code>password</code>with your credentials.
</aside>


As soon as the address list request is made, it is queued for address correction. Because the client must poll to determine if correction is complete, we suggest making this address list request first and then moving on with the succeeding steps to allow workflow in parallel.

The XML response looks like this:

`xml
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<addressList>
  <id>123</id>
  <status>0</status>
  <description>Uploaded</description>
  <statusUrl>https://rest.click2mail.com/molpro/addressLists/123
  </statusUrl>
</addressList>
`

### Possible return status

Status | Description
------- | ---------
0 |	Uploaded
1 |	Mapped
2 |	Created
3 |	CASS Standardized
9 |	Error Description
