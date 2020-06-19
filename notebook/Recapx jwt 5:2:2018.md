@grosz
## tl;dr

* JWT stands for "JSON Web Token"
* * This site has all you need: https://jwt.io/
* * They are a compact, signed and tamper proof way of sending data as "claims"
* * JWTs are (usually) just encoded, not encrypted, so the contents are readable by anyone
* * The tokens are URI safe, so nice and easy to pass in a query param
* * Can be signed with strong crypto, so trustworthy for servers that have the right keys
*
* ### A day in the life of a JWT
*
* Dan and I used Auth0 as a reference, and determined that the "right way" to handle authentication and authorization for a purely static Single Page App was using the "Implicit Grant" OAuth flow.
*
* https://auth0.com/docs/api-auth/which-oauth-flow-to-use
*
* 1) Server has already determined identity of a user and validated the client
* 2) Server generates a JWT and signs it
* 3) Sends the JWT via server side redirect to SPA
* 4) The SPA pulls some useful information from the token, but does NOT verify (there are no secrets in a static SPA)
* 5) The SPA just assumes it is correct, and shows the user "logged in" with whatever claims are in the token
* 6) The token is sent along as a Bearer token with all requests that require auth
* 7) The server verifies the token validity with the PK used to sign it
