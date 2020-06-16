# Authentication and Security

> Notes taken from udemy's course AngularJS Authentication: Secure your app with AuthO from Ryan Chenkie

- RESTful APIs may conflict with traditional authentication behaviour, setting sessions to store authorization cookies in client's side.
- In cookie-based authentication, sessions can't be easily shared.
- Cookies set a drawback in authentication when it comes to implementing the same API in multiple clients. As the data storage strategy needs to be defined for each different client's environment.

## JSON Web Tokens

- Transmit claims within a JSON payload
- Is an encoded token that comprises 3 parts separated by a point: 
	- Header. Algorithm and token type.
	- Payload. Data; custom claims can be added.
		- sub: user
		- iat: issued at
		- exp: expires at
	- Verify signature. encoded header and payload, and a secret encrypted in SHA256.

- JWOT gets attached in the HTTP Header `Authorization`:
	- `Authorization: Bearer <token>`

## Setup 

- Create an account and tenant in auth0.com
- Define callback URL (dev-owned location to validate authentication)
- Installing auth0 libraries. `npm install auth0-js angular-auth0`


> Written with [StackEdit](https://stackedit.io/).

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEwNjE3NjgwNjcsLTE5MTA3MTQwMjMsMj
k0ODU1NTA5XX0=
-->