# Create a Document


```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```shell
curl "http://example.com/api/kittens"
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let kittens = api.kittens.get();
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 1,
    "name": "Fluffums",
    "breed": "calico",
    "fluffiness": 6,
    "cuteness": 7
  },
  {
    "id": 2,
    "name": "Max",
    "breed": "unknown",
    "fluffiness": 5,
    "cuteness": 10
  }
]
```

```xml
   <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <job>
      <id>0</id>
      <status>9</status>
      <description>Invalid parameter guarantee.</description>
    </job>
```

Creates a new document in your account from an uploaded file.



### POST /documents

Creating new documents requires POSTing a request to:

`https://{username}:{password}@rest.click2mail.com/molpro/documents
/documentName = "Sample Letter"
/documentClass = "Letter 8.5 x 11"
/documentFormat = "PDF"
/file = "@{filename_of_pdf}"`

### URL Parameters

Parameter | Type | Description
--------- | ------- | -----------
documentClass	| Required |	Document Class
documentFormat	| Required |	Document format
documentName	| Optional|	Document name as it will be stored in your account

### Possible values of document format

Document Format |
------ |
PDF |
DOC |
DOCX |
PUB |
PPT |
PPTX |
ODT |
JPEG |
JPG | 
PNG |

A positive response will be a HTTP status 201 Created.
A negative response will be a HTTP status 400 Document Error.

The XML response looks like this:

`
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<documents>
  <id>12345</id>
  <status>0</status>
  <description>Success</description>
</documents>
`

### Possible return status

Status | Description
------- | ---------
0 |	Success
2 |	Document Dimensions outside of range
3 | The maximum number of pages for this product is xx
4 |	Could not render document
9 | The minimum number of pages for this product is xx
9 |	The document being uploaded cannot be read and is corrupt
