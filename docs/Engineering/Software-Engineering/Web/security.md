# Security

<h3>Table of Contents</h3>

[TOC]

# Encryption

Refer to [/Computer-Science/se#encryption](/Computer-Science/se#encryption)

# Hashing

aka Obfuscation

- puctuation matters while hashing Strings

|Algo|Date|Size<br>(bits)|Size<br>(bytes)|Length<br>(hex digits)|
|-|-|-|-|-|
|MD5|TODO|128|16|32|
|SHA-1|TODO|160|20|40|
|SHA-256|TODO|256|32|64|


## MD5



## SHA1

## SHA256

## PBKDF2

## SCrypt

## BCrypt

## Argon2

### Argon2i

### Argon2d

### Argon2id

## Ref

- https://medium.com/analytics-vidhya/password-hashing-pbkdf2-scrypt-bcrypt-and-argon2-e25aaf41598e


# Deidentifying PII

- [PII Anonymization/Deidentification Techniques](/Engineering/Software-Engineering/Product-Development/regulations_and_compliances#pii-anonymizationdeidentification-techniques)

# JWT

JSON Web Token

- a compact, URL-safe way/means of representing claims securely between two parties
    - URL-safe
        - 3 parts separated by dots
- open & industry standard
- [RFC 7519](https://tools.ietf.org/html/rfc7519)
    - status: concensus of IETF
- format intended for space constrained environments such as:
    - HTTP Authorization headers 
    - HTTP URI query parameters
- a string representing a set of claims as a JSON object that is encoded in a JWS or JWE, enabling the claims to be digitally signed or MACed and/or encrypted
    - can have zero or more claims
- a __signed__ JWT is an abstraction over either JWS or JWE

```json5
// Header: Algorithm and Token type
{
    "alg": "HS256",
    "typ": "JWT"
}

// Payload: Data
{
    "name": "John"
    "iat": 1615455676
}

// Signature 
some secret string // optionally base64/base64url encoded
```

## Base 64 Encoding
- binary to text encoding
- represents binary data (8-bit bytes) to ASCII string format
    - using radix-64 representation
- designed to carry data (binary data) across channels that only reliably supports text content


## Base 64 URL Encoding
First encode the string to base64, this may result in encoded string having some signs like `+`, `/`, `=` which have different meaning in filesystem/urls. Thus need to encoded them further to make them URL-safe.

Index|Base64|Base64Url
-----|------|-----
0|A|A 
1|B|B 
2|C|C 
3|D|D 
4|E|E 
5|F|F 
6|G|G 
7|H|H 
8|I|I 
9|J|J 
10|K|K 
11|L|L 
12|M|M 
13|N|N 
14|O|O 
15|P|P 
16|Q|Q 
17|R|R 
18|S|S 
19|T|T 
20|U|U 
21|V|V 
22|W|W 
23|X|X 
24|Y|Y 
25|Z|Z 
26|a|a 
27|b|b 
28|c|c 
29|d|d 
30|e|e 
31|f|f 
32|g|g 
33|h|h 
34|i|i 
35|j|j 
36|k|k 
37|l|l 
38|m|m 
39|n|n 
40|o|o 
41|p|p 
42|q|q 
43|r|r 
44|s|s 
45|t|t 
46|u|u 
47|v|v 
48|w|w
49|x|x
50|y|y
51|z|z
52|0|0
53|1|1
54|2|2
55|3|3
56|4|4
57|5|5
58|6|6
59|7|7
60|8|8
61|9|9
62|+|-
63|/|_
  |=|(optional)

## Parts of JWT

JWT is combination of 3 base64 url encoded strings, parted by 2 dots

### JOSE Header

- typ
    - defines the media type of the complete JWT
    - optional; recommended value: JWT
    - defined by JWT specifications
- cty
    - defines the content type; defines structural information
    - recommended to use in case of nested JWTs only
    - defined by JWT specifications
- alg
    - defined by JWS specifications
- kid
    - defined by JWS specifications

### Secret

### Payload/Body/Claim


## Claim
- a piece of information asserted about a subject
    - asserted: 
        - say something clearly and firmly
        - in determined and confident way
- key val pair
- key == always string
- val could be any JSON data type

## JWS
JSON Web Signature

## JWA

JSON Web Algorithm

- RFC 7518
- all applicable algorithms for signing are defined under this

## JWE
JSON Web Encryption

## Unsecured JWT

- is a JWS object without any algorithm (`alg: none`) in its JOSE header
- is a JWS w/o signature

## Ref
1. https://medium.facilelogin.com/jwt-jws-and-jwe-for-not-so-dummies-b63310d201a3


# Token-Based Authentication

# OpenID 1.0 

(2006) 

- lets an app ask an authority for proof that an end user owns an identity (a URL).
- an __Authentication__ protocol
- deprecated
- example
    - End user to app: I am Steve A. Smith.
    - App to authority: Is this Steve A. Smith?
    - The end user and authority speak for a moment.
    - Authority to app: Yes, that is Steve A. Smith.


# OpenID 2.0

(2007)

- does the same as OpenID 1.0, but adds a second identity format (XRI) and adds flexibility to how the end user specifies the identity and authority.
- an __Authentication__ protocol
- deprecated


# OpenID Attribute Exchange 1.0

(2007)

- extends OpenID 2.0 by letting an app fetch & store end user profile information with the authority - in addition to verifying the end user's identity.
- an __Authentication__ protocol
- deprecated
- example:
    - End user to app: I am Steve A. Smith.
    - App to authority: Is this Steve A. Smith? Oh, and if it is, also fetch me his email address and phone number.
    - The end user and authority speak for a moment.
    - Authority to app: Yes, that is Steve A. Smith. His email is steve@domain.com and phone number is 123-456-7890.


# OAuth 1.0

(2010)

- lets an end user grant an app limited access to resources on a third-party server that an authority owns.
- example:
    - App to end user: We'd like to access your pictures on some other server.
    - The end user and authority speak for a moment.
    - Authority to app: Here is an access token.
    - App to third-party server: Here is the access token that proves I am allowed to access pictures for an end user.
- an __Authorization__ protocol
- deprecated


# OAuth 2.0

(2012)

- does the same thing as OAuth 1.0 but with a completely new protocol
- an __Authorization__ framework

## Authorization Grant Types (Flow)

There are multiple ways in OAuth2.0 itself to achieve authorization, which are already specified in the RFC based on different client type/scenarios.

- Authorization Code Flow
- PKCE
- Client Credential
- Device Code
- Refresh Token
- Legacy: Implicit Flow
- Legacy: Password Grant

## Authorization Code Flow

This is a suitable flow for following kind of case.

### Participants

1. End User (2nd party)
1. Client (Mobile/SPA App - 3rd party)
1. Service Provider (Resource server - 3rd party, Authorization server knows this as Registered Client as well)
1. Authorization server (1st party)

Example: Toran wants to use Way2SMS App (and internally their server) to send SMS to all the contacts stored in his Google account. Here,

- End user = Toran
- Client = Way2SMS App
- Service Provider = Way2SMS server
- Authorization Server = Google

Where, the service provider is a 3rd party server. If there is no 3rd party server, and only Mobile/SPA clients, then PKCE is a better/secure flow. Even, now its recommended to use PKCE for 3rd party resource provider server case as well.

### Prerequisites

#### Setup of an Authorization Server

Authorization Base

    https://authorization-server/oauth2/authorize

Token URL

    https://authorization-server/oauth2/token/

Redirect URL

    https://authorization-server/oauth2/callback

Authorization URL

    https://authorization-server/oauth2/authorize/?response_type=code&state=random_state_string&client_id=:client_id


#### Register an Resource Provider Server as Client in Authorization Server

Input:

    client_type: confidential/public  (public for Mobile App, Web App; confidential for backends/servers)
    Authorization Grant Type: authorization-code
    Redirect URL: https://resource-provider/oauth2/callback

Output:

    client_id: BOqLOb2uaTn4ppi5nlj2ErTWpr9fKt5YQrwpDvfs
    client_secret: bamZTX1gknB99XZvKWYucUPVdY5Aum5k8LDoZzUWz0VhwaSZpFhCyUrrxshaAJKtaZ5bTJXimBCLgjs0yPZxvow9NBrqEXG6qeK0VFy2incKLzZdw97Q4jNxAafBq3c8

Keep note of this.

### Flow

#### 1. End-user opens Way2SMS App
#### 2. Writes a SMS and clicks on `Send to My Google Contacts`
#### 3. As End-user has not authorized the Way2SMS server (as well as app) to access End-user's resource stored at Google server
#### 4. Way2SMS server provides the Way2SMS app a link to redirect the End-user there to complete the authorization with Google OAuth2 server
1. The shared URL (called Authorization API) by Way2SMS server has a few query params appended by the Way2SMS server

```
GET https://authorization-server/oauth2/authorize?response_type=code&state=random_state_string&client_id=:client_id&redirect_url=<https://service-provider/oauth2/callback>&scope=profile%20email
```

##### Parameters

Name|Type|In|Description
---|----|--|----------
client_id|string|query|ID of the service provider server (Way2SMS server), that is registered with Google OAuth Serverredirect_url|string|query|(optional)url-encoded URL/API of service provider server where the OAuth server should redirect after authorization - it should match the previously registered redirect url at authorization server
response_type|string|query|indicates the expectation in return i.e. an authorization code
state|string|query|any state encoded as JWT if maintained by service provider which should be send back to it by authorization server after authorization
scope|string|query|(optional)space separated scope to request additional level of access - depends on particular service

Note: 

1. Here `state` may serve multiple purposes:
    1. Serves as a CSRF protection mechanism if it contains a random value per request. When the user is redirected back to your app, double check that the state value matches what you set it to originally.
    1. This may be used to indicate what action in the app to perform after authorization is complete, for example, indicating which of your app’s pages to redirect to after authorization.
    1. This gives your app a chance to persist data between the user being directed to the authorization server and back again, such as using the state parameter as a session key.
1. Some services support registering multiple redirect URLs, and some require the redirect URL to be specified on each request. Check the service’s documentation for the specifics.



#### 5. Way2SMS app opens this URL in app/browser, if not already logged-in, then it shows a Login Form
#### 6. End-user had to enter their Google credentials
#### 7. Once the credentials are validated, it shows that the service provide (Way2SMS server) wants to access this. this and this, do you consent?
#### 8. If end-user accepts and agrees on the consent then in return Google authorization server redirects the end-user to the registered redirect_url by appending an "authorization code" to it

```
GET https://service-provider/oauth2/callback?code=:code&state=random_state_string"
```

##### Parameters

Name|Type|In|Description
----|----|--|----------
code|string|query|Authorization code, an intermediary step of getting access token from OAuth Server
state|string|query|any state encoded as JWT if maintained by service provider which is sent back to it by authorization server after authorization

Note: 

1. Authorization Code is single-use (temporary) code
1. As the Authorization Code is being sent by the OAuth server through GET query param - its visible to everyone (End-user, Way2SMS client, Way2SMS server)

##### Response

This depends how resource server has coded its `GET /oauth2/callback` API

I would say, just show an JSON response with Authorization Code.

```json
{
    "code": "<authorization code>"
}
```

Note: The service provider (Way2SMS server) has already received the authorization `code` & `state`. Its just doing an adhoc work of showing the `code` as response - if it does not, then also its fine.

#### 9. Now the service provider server (Way2SMS server) has the authorization code (also, if required, then Way2SMS App can provide the same through some helper API of Way2SMS server)

#### 10. Service provider server can now call authorization server to get an access code in exchange of authorization code, by supplying a few important details about the registered service provider server

    POST https://authorization-server/oauth2/token/

##### Parameter

Name|Type|In|Description
----|----|--|-----------
Content-Type|string|header|Content-Type is responsible for telling the HTTP client or server what type of data is being sent
grant_type|string|body|The type of grant flow we are using in this case `authorization_code`
client_id|string|body|ID of the application that is registered with OAuth Server
client_secret|string|body|This is generated along with client id when registering the user with OAuth Server
code|string|body|The code which we got back from when we hit authorize url of our OAuth Server

Note: 

1. The request along with `code` will be authorized by `client_secret`. It may check a) if the `client_id` is correct & registered or not; b) if so, then the `code` is generated by that `client_id` or not etc.
1. `client_secret` adds an extra security layer. so that even if the `code` gets intercepted by someone - it could not be utilized without a valid `client_secret`
1. The `client_id` & `client_secret` could be passed as HTTP Basic Authentication, in a few authorization servers, check respective docs.

#### Response

```json
{
    "access_token": "rzKuDDYGSiNIJWuz6hJJc0n5NatPM5", 
    "expires_in": 10800, 
    "token_type": "Bearer", 
    "scope": "read write groups introspection", 
    "refresh_token": "1PnkGf9PQfG7urgXx1JCXYAtBpB3mf"
}
```

##### Parameter

Name|Type|In|Description
----|----|--|-----------
access_token|string|body|the access token itself, which we will use to query resource in resource server
expires_in|int|body|It is an integer representing the TTL of the access token (i.e. when the token will expire)
token_type|string|body|This will usually be the word “Bearer” (to indicate a bearer token). Possession of the bearer token is considered authentication.
scope|string|body|the scope is a way to restrict access to specified areas e.g. profile, email, group etc
refresh_token|string|body|a refresh token that can be used to acquire a new access token when the original expires

Note: As the service provider (Way2SMS server/resource provider) is calling this API in backend, and receiving access token as response - its totally hidden from anyone else (i.e. Way2SMS App, End-user, any Middle-man)


#### 11. Now, the service provider (Way2SMS server) can access the Google contacts of the End-user by supplying the access token


```
$ curl \
--header "Authorization: Bearer <access_token>" \
--header "Content-Type: application/json" \
--request GET \
--url http://authorization-server/v1/contacts \
```

### Response

```
{
	"contacts": [...]
}
```

### Extra Possible Flows


#### 1. Service Provider can Introspect an Access Token

```
$ curl \
--header "Content-Type: application/x-www-form-urlencoded" \
--request POST \
--url https://authorization-server/oauth2/introspect/ \
--data '{
"token": "<access_token>",
"client_id": "<client_id>",
"client_secret": "<client_secret>"
}'
```

##### Parameters

Name|Type|In|Description
----|----|--|-----------
access_token|string|body|the access token itself, which we will use to query resource in resource server
client_id|string|body|ID of the application that is registered with OAuth Server
client_secret|string|body|This is generated along with client id when registering the user with OAuth Server

##### Response
```
{
	"active": false
}
```


#### 2. Service Provider can Revoke an Access Token

```
$ curl \
--header "Content-Type: application/x-www-form-urlencoded" \
--request POST \
--url http://authorization-server/oauth2/revoke_token/ \
--data '{
"token": "<access_token>",
"token_type_hint": "access_token",
"client_id": "<client_id>",
"client_secret": "<client_secret>"
}'
```

##### Parameters

Name|Type|In|Description
----|----|--|-----------
access_token|string|body|the access token itself, which we will use to query resource in resource server
token_type_hint|string|body|(optional) designating either ‘access_token’ or ‘refresh_token’
client_id|string|body|ID of the application that is registered with OAuth Server
client_secret|string|body|This is generated along with client id when registering the user with OAuth Server


### Response

```
HTTP 200

{}
```


#### 3. Service Provider can Refresh an Access Token

```
$ curl \
--header "Content-Type: application/x-www-form-urlencoded" \
--request POST \
--url https://authorization-server/oauth2/token/ \
--data '{
"grant_type": "refresh_token",
"refresh_token": "<refresh_token>",
"client_id": "<client_id>",
"client_secret": "<client_secret>"
}'
```

##### Parameters

Name|Type|In|Description
----|----|--|-----------
refresh_token|string|body|the access token itself, which we will use to query resource in resource server
grant_type|string|body|this mentions that get me new access_token in exchange of refresh_token - by calling the same token API
client_id|string|body|ID of the application that is registered with OAuth Server
client_secret|string|body|This is generated along with client id when registering the user with OAuth Server



##### Response

```json
{
    "access_token": "<your_new_access_token>",
    "token_type": "Bearer",
    "expires_in": 36000,
    "refresh_token": "<your_new_refresh_token>",
    "scope": "read write"
}
```

## Ref
1. https://www.oauth.com/oauth2-servers/server-side-apps/authorization-code/
1. https://oauth.net/2/

## PKCE

(Proof Key for Code Exchange, pronounced pixie)

### Why
Single-page apps (or browser-based apps) run entirely in the browser after loading the Javascript and HTML source code from a web page. Since the entire source is available to the browser, they cannot maintain the confidentiality of a client secret, so the secret is not used for these apps. The flow is exactly the same as the authorization code flow, but at the last step, the authorization code is exchanged for an access token without using the client secret.

Because of this, Single-page apps (or browser based apps) must use an OAuth flow that does not require a client secret. Or, say does not require a predefined client secret.

### What
PKCE (RFC 7636) is an extension to the Authorization Code flow to prevent several attacks and to be able to securely perform the OAuth exchange from public clients.

### How
This extension describes a technique for public clients to mitigate the threat of having the authorization code intercepted. The technique involves the client first creating a secret, and then using that secret again when exchanging the authorization code for an access token. This way if the code is intercepted, it will not be useful since the token request relies on the initial secret.

Note: Post 2019, its recommended for confidentical clients (backend/servers) using Authorization Code Flow to follow PKCE.

## Ref
1. https://www.oauth.com/oauth2-servers/pkce/
1. https://www.oauth.com/oauth2-servers/single-page-apps/
1. https://www.oauth.com/oauth2-servers/mobile-and-native-apps/
1. https://www.oauth.com/oauth2-servers/server-side-apps/authorization-code/
1. https://oauth.net/2/


## Implicit Flow

Some services use the alternative Implicit Flow for single-page apps, rather than allow the app to use the Authorization Code flow with no secret.

The Implicit Flow bypasses the code exchange step, and instead the access token is returned in the query string fragment to the client immediately.

In order for a single-page app to use the Authorization Code flow, it must be able to make a POST request to the authorization server. This means if the authorization server is on a different domain, the server will need to support the appropriate CORS headers. If supporting CORS headers is not an option, then the service may use the Implicit Flow instead.

### Ref
1. https://www.oauth.com/oauth2-servers/single-page-apps/


# OpenID Connect

(2014)

- combines the features of OpenID 2.0, OpenID Attribute Exchange 1.0, and OAuth 2.0 in a single protocol. It allows an application to use an authority...
    - to verify the end user's identity,
    - to fetch the end user's profile info, and
    - to gain limited access to the end user's stuff.
- an __Authorization__ as well as __Authentication__ protocol

# OAuth, OpenID, OpenID Connect

1. OpenID is about verifying a person's identity (authentication).
1. OAuth is about accessing a person's stuff (authorization).
1. OpenID Connect does both.

All three let a person give their username/password (or other credential) to a trusted authority instead of to a less trusted app.


# SAML
- https://gravitational.com/blog/how-saml-authentication-works/
- https://en.wikipedia.org/wiki/SAML_2.0#SP_redirect_request;_IdP_POST_response
- https://docs.oasis-open.org/security/saml/v2.0/saml-bindings-2.0-os.pdf
- http://docs.oasis-open.org/security/saml/Post2.0/sstc-saml-tech-overview-2.0-cd-02.html#5.1.2.SP-Initiated%20SSO:%20%20Redirect/POST%20Bindings|outline
- http://docs.oasis-open.org/security/saml/Post2.0/sstc-saml-tech-overview-2.0-cd-02.html#5.1.3.SP-Initiated%20SSO:%20%20POST/Artifact%20Bindings|outline
- http://saml.xml.org/saml-specifications
- http://saml.xml.org/wiki/sp-initiated-single-sign-on-postartifact-bindings
- http://saml.xml.org/wiki/idp-initiated-single-sign-on-post-binding
- http://docs.oasis-open.org/security/saml/v2.0/saml-core-2.0-os.pdf (3.4.1 Element <AuthnRequest>) for schema details
- https://blogs.oracle.com/dcarru/sp-vs-idp-initiated-sso
- Azure: 
	- AuthnRequest: https://docs.microsoft.com/en-us/azure/active-directory/develop/single-sign-on-saml-protocol#authnrequest
	- Claims: https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-saml-claims-customization
	- SSO: https://docs.microsoft.com/en-us/azure/active-directory/manage-apps/what-is-single-sign-on#saml-sso
	- Setup: https://docs.microsoft.com/en-us/azure/active-directory/manage-apps/configure-single-sign-on-non-gallery-applications
	- Error AADSTS750054: https://docs.microsoft.com/en-us/azure/active-directory/manage-apps/application-sign-in-problem-federated-sso-gallery#saml-request-not-present-in-the-request
	- Test SAML: https://docs.microsoft.com/en-us/azure/active-directory/azuread-dev/howto-v1-debug-saml-sso-issues
- Okta:
	SAML: https://developer.okta.com/docs/concepts/saml/
- OneLogin
	- https://www.samltool.com/generic_sso_req.php
	- https://developers.onelogin.com/saml/python
	- https://github.com/onelogin/python3-saml
	- AuthnRequest: https://developers.onelogin.com/saml/examples/authnrequest
	- SAMLRequest
		- https://github.com/onelogin/python3-saml/blob/a11c34103e0aa75ee1930471c492b5f8f69962c0/src/onelogin/saml2/auth.py#L378-L379
	- Setup
		- https://support.templafy.com/hc/en-us/articles/115005026225-How-to-setup-SSO-with-OneLogin-SAML-
	- Test
		- https://onelogin.service-now.com/support?id=kb_article&sys_id=83f71bc3db1e9f0024c780c74b961970
- StackOverflow
	- https://stackoverflow.com/questions/30388926/http-redirect-binding-saml-request
- Tools
	- deflate + b64emcode: https://www.samltool.com/encode.php
	- urlencode: https://www.urlencoder.org/

# Secret Management

## A few other factors to keep in mind:

1. The secret should update/reflect (always latest) in a job/batch pipeline if rotated?
1. The secret should update/reflect (always latest) in a service/streaming pipeline if rotated?
1. The secret could be fixed be locked/fixed in two ways: a) By mentioning a particular secret version, b) by not updating the secret on rotations
1. The secret version info should be available/accessible for audit logging/record keeping? 
1. If secret rotated, the secret version should also get updated - should not be stale one?
1. The past/historical version of the secrets should be available at any time?

## Secret Managers Options

- AWS Secret Manager
- GCP Secret Manager
- Hashicorp Vault
- Kubernetes Secrets

## Secret Delivery mechanisms

- As file system
    - Mount as volume
        - Secrets should be accesible as files
        - Freshness?
            - With update the file when secret rotated
            - With check for update and update the file when secret is accessed
- Set as Environment Variable
    - Once set can't be rotated, need custom logic to update
- Use the API client to always fetch the secret from manager
     - May cache it locally to save frequent call, but cache invalidation has to be handled at own
     - May concern the team when a set of apps are deployed together and all of them started calling the API server concurrently

## Hashicorp Vault

- Comes with
    - template rendering option using consul-template CLI
    - API client
- consul-template is capable to detect a secret rotation through SIGNALs
- consul-template & vault both are highly configurable

## GCP Secret Manager

- Uses may differ per GCP service, e.g. Google Compute Engine, Cloud Function, Cloud Run, GKE, Dataflow etc.
- Comes with
    - API client
- Google recommend using the Secret Manager API directly (using one of the provided client libraries, or by following the REST or GRPC documentation), because:
    - When a secret is accessible on the filesystem, application vulnerabilities like directory traversal attacks can become higher severity as the attacker may gain the ability to read the secret material.
    - When a secret is consumed through environment variables, misconfigurations such as enabling debug endpoints or including dependencies that log process environment details may leak secrets.
- Ref:
    - https://cloud.google.com/run/docs/configuring/secrets
    - https://cloud.google.com/secret-manager/docs/best-practices
    - https://cloud.google.com/secret-manager/docs/using-other-products
    - https://cloud.google.com/secret-manager/docs/accessing-the-api
    - Access using:
        - [Native libraries](https://cloud.google.com/secret-manager/docs/reference/libraries)
        - [gcloud CLI](https://cloud.google.com/sdk/gcloud/reference/secrets)
        - [REST API](https://cloud.google.com/secret-manager/docs/reference/rest)
        - [RPC API](https://cloud.google.com/secret-manager/docs/reference/rpc)

### Use in GKE
- Access GCP Secrets feature is implemented using https://github.com/GoogleCloudPlatform/secrets-store-csi-driver-provider-gcp
- Supports Mount as filesystem & Set as environment var
- Not officially supported by Google 
- Secret rotation & sync feature is in Alpha
- Read [Security considerations](https://github.com/GoogleCloudPlatform/secrets-store-csi-driver-provider-gcp#security-considerations)

### Use in Cloud Run
- https://stackoverflow.com/questions/68533094/how-do-i-access-mounted-secrets-when-using-google-cloud-run

## AWS Secret Manager

- https://pkg.go.dev/github.com/chrissav/consul-template-plugin-secretsmanager
