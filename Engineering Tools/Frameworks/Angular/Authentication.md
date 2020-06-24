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
- Depdendency is injected using `auth0.auth0`, `angularAuth0Provider`

Base configuration
````javascript
function config(...,$stateProvider, ...){
	$stateProvider
	.state('callback', {
	   url: '/callback',
	   controller: 'CallbackController',
	   templateUrl: 'app/callback/callback.html'
	});
} 
````

## Usage
Init service:
```javascript
angularAuth0Provider.init({
	clientID: <id>,
	domain: 'host.auth0.com',
	# token is the access token
	responseType: 'token id_token',
	redirect_uri: 'http://localhost.com:3000/callback',
	scope: 'openid'
});
```
Defining a service that calls and handles authentication process

```javascript
function authService($state, angularAuth0, $timeout){
	function login(){
		angularAuth0.authorize();
	}
	
	function handleAuthentication(){
		angularAuth0.parseHash(function(err, authResult){
			if (authResult && authResult.accessToken && authResult.idToken){
				setSession(authResult);
				console.log(authResult);
			}
		});
	}

	function setSession(authResult){
		var expiresAt = JSON.stringify(
			(authResult.expiresIn *1000 + new Date().getTime())
		);
		localStorage.setItem('access_token', authResult.accessToken);
		localStorage.setItem('id_token', authResult.idToken);
		localStorage.setItem('expires_at', expiresAt);
	}

	// based on the expiry date of the access token
	function isAuthenticated(){
		var expiresAt = JSON.parse(localStorage.getItem('expires_at'));
		return new Date().getTime() < expiresAt;
	}
}
```

JSON web token is then sent as a Bearer Header to obtained access to protected resources.

##  Setting up JWT Provider

```javascript
angular
  .module('app', [..., 'angular-jwt'])
  .config(config);

config.$inject = [
  ...
  'jwtOptionsProvider'
];

...
config(..., jwtOptionsProvider){
   jwtOptionsProvider.config({
		tokenGetter: function(){
           return localStorage.getItem('access_token');
        },
        whiteListedDomains: ['localhost']
    });
    $httpProvider.interceptors.push('jwtInterceptor');
});
```

> Written with [StackEdit](https://stackedit.io/).

<!--stackedit_data:
eyJoaXN0b3J5IjpbMTQwMTU4MTA2OCwtMjMyNDk1NjI3LC01ND
k5NDgzNzksMTc5MzM1OTU1LC0yMDMyMTI2NTA4LC0xMDYxNzY4
MDY3LC0xOTEwNzE0MDIzLDI5NDg1NTUwOV19
-->