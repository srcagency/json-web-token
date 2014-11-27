# json-web-token

JWT encode and decode for Node.js that can use callbacks or by returning an object `{error:, value:}`


**code coverage:**  
`npm test && npm run check-coverage && npm run coverage`

**codestyle:** 	
`npm run codestyle`

**jshint:** 	
`npm run jshint`

**WIKI**

JSON Web Token (JWT) is a compact URL-safe means of representing claims to be transferred between two parties. The claims in a JWT are encoded as a JavaScript Object Notation (JSON) object that is used as the payload of a JSON Web Signature (JWS) structure or as the plaintext of a JSON Web Encryption (JWE) structure, enabling the claims to be digitally signed or MACed and/or encrypted. 

[info](http://tools.ietf.org/html/draft-ietf-oauth-json-web-token-08) & [more info](http://self-issued.info/docs/draft-jones-json-web-token-01.html)


<a href="https://nodei.co/npm/json-web-token/"><img src="https://nodei.co/npm/json-web-token.png?downloads=true"></a>

[![Build Status](https://travis-ci.org/joaquimserafim/json-web-token.png?branch=master)](https://travis-ci.org/joaquimserafim/json-web-token)



**V1.2**




###API
  
  
#####  jwt#encode(key, payload, [algorithm], cb)
  
* **key**, your secret
* **payload**, the payload or Claim Names, 

	ex:
	
		{
		  "iss": "my_issurer",
		  "aud": "World",
		  "iat": 1400062400223,
		  "typ": "/online/transactionstatus/v2",
		  "request": {
		    "myTransactionId": "[myTransactionId]",
		    "merchantTransactionId": "[merchantTransactionId]",
		    "status": "SUCCESS"
		  }
		}

	*attention that exists some reserved claim names (like "iss", "iat", etc..) check [in here](http://tools.ietf.org/html/draft-ietf-oauth-json-web-token-08#section-4) for more info about JWT Claims.*	
* **algorithm**, default to 'sha256', use *jwt#getAlgorithms()* to get the supported algorithms
* **cb**, the callback(err[name, message], token)


#####  jwt#decode(key, token, cb)

* **key**, your secret
* **token**, the JWT token
* **cb**, the callback(err[name, message], payloadDecoded)


#### Example

	var jwt = require('json-web-token');
	
	var payload = {
	  "iss": "my_issurer",
	  "aud": "World",
	  "iat": 1400062400223,
	  "typ": "/online/transactionstatus/v2",
	  "request": {
	    "myTransactionId": "[myTransactionId]",
	    "merchantTransactionId": "[merchantTransactionId]",
	    "status": "SUCCESS"
	  }
	};
	
	var secret = 'TOPSECRETTTTT';
	
	// encode
	jwt.encode(secret, payload, function (err, token) {
	  if (err) {
	  	return console.error(err.name, err.message);
	  } else {
	  	console.log(token);

		// decode
	  	jwt.decode(secret, token, function (err_, decode) {
	    	if (err) {
	  			return console.error(err.name, err.message);
	  		} else {
	    		console.log(decode);
	    	}
	  	});
	  }
	});

