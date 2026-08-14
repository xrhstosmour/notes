#caching #architecture #performance

Where the cache sits relative to the application and the database determines who's responsible for keeping it correct.

## Cache-Aside (Lazy Loading)

The application checks the cache first, on a miss it reads from the database and populates the cache itself.

- Simple, only what's actually requested gets cached.
- Every miss costs a database round trip, and nothing guarantees the cache stays fresh on writes, that's the application's job.

## Read-Through

Same lookup order as cache-aside, but the cache itself owns the database read on a miss, not the application.

- Application code doesn't need to know about the database at all for reads.
- Adds a layer of indirection and latency to every miss, more setup than cache-aside.

## Write-Around

Writes go straight to the database, bypassing the cache. The cache only fills in on a subsequent read (a miss).

- Keeps the cache from filling with data that's written once and rarely read.
- A read immediately after a write is guaranteed to miss.

## Write-Back (Write-Behind)

Writes land in the cache first, and are flushed to the database asynchronously in the background.

- Fast writes, absorbs write bursts without hammering the database.
- If the cache dies before a flush, that write is gone, needs a durable queue or replication to be safe.

## Write-Through

Every write goes to the cache and the database at the same time, synchronously.

- Cache and database can't drift, simplest consistency story.
- Every write pays the cost of both a cache write and a database write.

## Thundering Herd / Dog-Pile Mitigation

When a hot cache key expires, many concurrent requests can all miss at once and hammer the database trying to regenerate the same value.

A common fix: extend the entry's TTL by a grace window the moment it's found expired, so the first process to notice regenerates the value while everyone else keeps serving the stale one during that window. Once the new value is written, subsequent reads pick it up. Rails' `ActiveSupport::Cache` option `race_condition_ttl` implements exactly this, but the pattern applies to any cache, not just Rails.
