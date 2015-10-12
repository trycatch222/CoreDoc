# HRW Core REST API Authentication

## Introduction

MyHRW Core uses Access Keys to ensure a secure access to it's REST interface.

MyHRW distinguishes 2 different Access Keys in it's authentication mechanism.

*  __The API key__ (or Application key) is a token which identifies a consumer of the Web Service which shall be present in the header of each request and as such travel over the network.

*  __The Secret Key__ which is use to encrypt the request signature on the client side. By definition the Secret key is hold by the consumer and shall never travel over the network.

## Anatomy of a MyHRW Request header

Sample:
```
 _X-NGA-ApiKey_: 1b51512A2Ed80181f1ac213B7062d3d4  
 _X-NGA-Signature_: hw6DY/ALURwuG6ARdhPwpktNG6FP8QVrqpC4vrW7I7g=  
 _X-NGA-Timestamp_: 2014-01-23T10:45:45Z  
_Content-Type_: application/json

```

1.  __The API key:__ Provided by the MyHRW team 
2.  __The signature:__ Composed and encripted signature see bellow 
3.  __The timestamp:__ Time of the call (ISO formated YYYY-MM-DDThh:mm:ss.sTZD), Time is expressed in UTC (Coordinated Universal Time), with a special UTC designator ("Z"). 
4.  __The format of the body:__ Always JSON 

## How to sign a request

### Compose the message

To sign a request, the caller should:

1. Build the signature string composed as explained below
2. Hashed the composed signature string with the secret key with HMAC SHA256 algorythm.   
3. Add the element in the request header as described in the previous point.

### Composition of the signature string 

The signature string is composed as follows:

1. METHOD: always uppercase e.g. GET, PUT, POST, ... 
2. Absolute URI path (lower case, url decoded)
3. Querystring (ordered by key, url decoded)
4. API Key (uppercase)
5. Timestamp (ISO formatted, Time is expressed in UTC, with the special UTC designator "Z".)

Example:

GET /api/test/hello?lastname=doe&firstname=john

```
"GET" + "\n" + "/api/test/hello" + "\n" + "firstname=john&lastname=doe" + "\n" + "application key" + "\n" + "2013-07-26T11:36:23Z"
```

POST /api/ticket/321654987 

```
"POST" + "\n" + "/api/ticket/321654987" + "\n" + "" + "\n" + "application key" + "\n" + "2013-07-26T11:36:23Z"
```
Remark : Even if you don't have any query string in the url, you still have to add the correct new line in the created string

##Example

Creating the signature un Perl
```perl
use Digest::SHA 'hmac_sha256_base64'; 

$verb = 'POST';
$fullPath = '/api/tickets';
$queryString = '';
$apiKey = uc 'aa79D2A6516684443e7e96b28A77f789';
$timestamp = '2015-08-03T11:29:49';
 
$secretKey = '67BF60a15b30DE292';
 
$message = join "\n", ($verb, $fullPath, $queryString, $apiKey, $timestamp);
$signature = hmac_sha256_base64($message, $secretKey);
 
```

Creating the signature in C# 

```csharp

var signature = "POST" + "\n" + "/api/tickets" + "\n" + "" + "\n" + "AA79D2A6516684443E7E96B28A77F789" + "\n" + "2015-08-03T11:29:49";

signature = ComputeHash("67BF60a15b30DE292", signature);

private static string ComputeHash(string secretKey, string message)
{
	var key = Encoding.UTF8.GetBytes(secretKey);
	string hashString;

	using (var hmac = new HMACSHA256(key))
	{
		var hash = hmac.ComputeHash(Encoding.UTF8.GetBytes(message));
		hashString = Convert.ToBase64String(hash);
	}

	return hashString;
}
```

Encoding the signature in Ruby

```ruby
def sign_hmac_sha256(secret_key, message)
	hash  = OpenSSL::HMAC.digest('sha256', secret_key, message)
	Base64.encode64(hash).strip()
end
```



Encoding the signature in JavaScript

```javascript
var crypto = require('crypto');

function ComputeHash(secretKey, message)
{
  return crypto.createHmac('sha256', secretKey).update(message).digest('base64');
}
```

## Privacy & Policies

See [Privacy & Policies](/docs/PrivacyAndPolicies)