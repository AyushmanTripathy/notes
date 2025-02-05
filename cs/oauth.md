# OAuth v2

Open Auhorization Protocol  
You authorise a application to use resources of another application on your behalf, without giving your credentials.

### Parties

1. Resource Owner
1. Client
1. Authorization Server
1. Resource Server

### Terms

1. Scope, granular permissions
1. Response Type, is generally `code` meaning authorization code.
1. Authorization code, temporary code granted after consent
1. Access Token, is not understood by client, used for using RS. 

## OAuth Flow

0. client obtains client id, client secret from AS
1. RO initiates with client
1. client redirects to AS with
    - client id
    - redirect URI
    - response type
    - scope
1. AS authentications RO
1. AS presents a consent form based on scopes to the RO
1. AS redirects to client with
    - Authorization code
1. client requests AS with
    - Authorization code
    - client id
    - client secret
1. AS responds with
    - access token
1. client uses access token to use RS

## OIDC (OpenId Connect)

- helps client to authenticate RO  
- also called SSO (Single Sign on)
- here instead of only access token client receives `identity`.
- hence AS is also called identity provider

### OIDC Flow

1. client uses a `openid` scope
1. client receives a id token along with a access token
1. id token 
