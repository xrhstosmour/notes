#api #authentication #security #oauth #jwt

Common ways an API authenticates a client, roughly ordered from simplest to most capable.

## API Key

A static string sent in a header or query parameter, the server checks it against a stored value.

``` bash
curl -H "X-API-Key: <api-key>" https://api.example.com/data
```

Never hardcode a key in frontend/mobile code, anything shipped to a client can be extracted, treat it as public.

## Basic Auth

Username and password, Base64-encoded, sent in the `Authorization` header on every request.

``` bash
curl -H "Authorization: Basic <base64(username:password)>" https://api.example.com/login
```

Credentials go out on every request, only acceptable over HTTPS, and even then mostly limited to internal/service-to-service use.

## OAuth 2.0

An authorization framework for delegating access without sharing a password. Five standard flows:

- Authorization Code: the standard flow for web apps, a redirect-based exchange of a short-lived code for a token.
- Client Credentials: server-to-server, no user involved.
- Implicit: deprecated, returned tokens directly from the redirect, superseded by Authorization Code + PKCE for SPAs.
- Password Grant: the client collects the user's password directly, avoid, defeats the purpose of OAuth.
- Device Authorization: for input-constrained devices (TVs, IoT), the user authorizes on a second device.

Authorization Code flow, simplified:

1. Client redirects the user to the authorization server.
2. User logs in and approves, authorization server redirects back with a code.
3. Client exchanges the code (plus its client secret) for an access token.
4. Client uses the access token on subsequent API calls.

``` bash
curl -X POST https://auth.example.com/token \
  -d grant_type=authorization_code \
  -d code=<auth-code> \
  -d client_id=<client-id> \
  -d client_secret=<client-secret>
```

## Bearer Token

Whatever token an OAuth2 flow (or similar) issued, sent as-is in the `Authorization` header, the server validates it and doesn't care how it was obtained.

``` bash
curl -H "Authorization: Bearer <access-token>" https://api.example.com/protected
```

Keep tokens short-lived and use a refresh token to mint new ones, rather than issuing long-lived access tokens.

## JWT

A self-contained, signed token (`header.payload.signature`) that encodes claims about the user directly, so the server can verify it without a database lookup.

- Never store a JWT in `localStorage`, it's readable by any script on the page, so an XSS bug becomes a token theft. Use an `HttpOnly` cookie instead.
- Keep expiration short, a compromised JWT is valid until it expires, there's no server-side revocation without extra bookkeeping.

## Session Cookies

A session ID is created on login and stored server-side, the cookie just references it.

```
Set-Cookie: session_id=<id>; HttpOnly; Secure; SameSite=Strict
```

Vulnerable to CSRF without `SameSite`, and to XSS-driven theft without `HttpOnly`.

## Comparison

| Method | Typical use case | Notes |
| --- | --- | --- |
| API Key | Simple/internal APIs | No user identity, easy to leak |
| Basic Auth | Internal/service-to-service | Credentials on every request |
| OAuth2 | Third-party access, delegated auth | Most setup, most capability |
| Bearer Token | Any token-based API | Format-agnostic, just a carrier |
| JWT | Stateless auth | Self-contained, hard to revoke early |
| Session Cookie | Traditional web apps | Server holds state, easy to revoke |
