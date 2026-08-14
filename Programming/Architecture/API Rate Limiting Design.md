#api #architecture #rate-limiting #security

Layering a coarse, fast edge-level limit with a slower, more precise application-level quota avoids the cost of exact real-time enforcement while still catching abuse.

## Edge Layer

A reverse proxy (e.g. nginx) enforces a simple per-token rate limit (e.g. 100 requests/minute). Fast, but has no application-level knowledge, it can't apply a different limit per client or track usage across a longer window like a day.

## Application Layer

Track usage in a fast store (e.g. Redis) as requests come in, and periodically sync counts to a durable store (e.g. once an hour) rather than writing to the database on every request.

A periodic job, not a per-request check, compares each client's usage against its configured daily limit and disables any client that's over. Disabling:

- Expires all of that client's active access/refresh tokens immediately.
- Returns a clear rate-limit error if the client tries to generate a new token while disabled.
- Gets automatically lifted by a second daily job (e.g. at midnight), unless the client was disabled manually, in which case it stays disabled until a human re-enables it.

This trades a small amount of burst tolerance (a client can burst right up to the enforcement job's next run) for avoiding a real-time quota check on every single request.

## Trusted Clients

Add an allowlist flag for clients that are exempt from the automatic limit entirely (e.g. after agreeing to different terms), so the default limit can stay conservative without needing manual intervention for every legitimate high-volume client.

## Observability

Log every rate-limit violation, client, request count, active token count at the time, somewhere visible to whoever owns the API, so patterns of abuse are traceable even though enforcement itself is asynchronous.
