#database #snowflake #ids #distributed-computed #postgresql
Snowflake IDs, or snowflakes, are a form of unique identifier used in distributed computing. The format was created by Twitter. Further details can be found [here](https://abheist.com/twitter-snowflake-for-unique-ids/)

## Structure

The canonical (Twitter) Snowflake ID is a 64-bit integer split into:

| Bits | Component | Description |
| ---- | --------- | ------------ |
| 1 | Sign bit | Always `0`, keeps the ID positive |
| 41 | Timestamp | Milliseconds since a custom epoch |
| 5 | Datacenter ID | Up to 32 datacenters |
| 5 | Machine ID | Up to 32 machines per datacenter |
| 12 | Sequence | Counter for IDs generated within the same millisecond |

The function below uses a simplified variant with a single combined `shard_id` instead of separate datacenter/machine fields.

In PostgreSQL you can generate Snowflake IDs via the following function:
``` sql
-- Create public schema if not exists.
CREATE SCHEMA IF NOT EXISTS PUBLIC;

-- Create sequence if not exists.
CREATE SEQUENCE IF NOT EXISTS PUBLIC.global_snowflake_id_sequence;

-- Create or replace function.
CREATE OR REPLACE FUNCTION PUBLIC.generate_snowflake_id(OUT result BIGINT) AS $$
DECLARE epoch bigint := 1314220021721;
sequence_id bigint;
milliseconds bigint;
-- The id of this database shard, must be set differently, for each schema.
shard_id int := 1;
BEGIN
SELECT nextval('PUBLIC.global_snowflake_id_sequence') % 1024 INTO sequence_id;
SELECT FLOOR(
        EXTRACT(
            EPOCH
            FROM clock_timestamp()
        ) * 1000
    ) INTO milliseconds;
result := (milliseconds - epoch) << 23;
result := result | (shard_id << 10);
result := result | (sequence_id);
END;
$$ LANGUAGE PLPGSQL;
```

## Python Reference Implementation

``` python
import time

class SnowflakeIDGenerator:
    def __init__(self, datacenter_id, machine_id, epoch=1609459200000):
        self.epoch = epoch
        self.datacenter_id = datacenter_id
        self.machine_id = machine_id
        self.sequence = 0
        self.last_timestamp = -1

    def _current_timestamp(self):
        return int(time.time() * 1000)

    def _wait_for_next_millisecond(self, last_timestamp):
        timestamp = self._current_timestamp()
        while timestamp <= last_timestamp:
            timestamp = self._current_timestamp()
        return timestamp

    def generate_id(self):
        timestamp = self._current_timestamp()

        if timestamp < self.last_timestamp:
            raise Exception("Clock moved backwards!")

        if timestamp == self.last_timestamp:
            self.sequence = (self.sequence + 1) & 0xFFF  # 12-bit mask.
            if self.sequence == 0:
                timestamp = self._wait_for_next_millisecond(self.last_timestamp)
        else:
            self.sequence = 0

        self.last_timestamp = timestamp

        return ((timestamp - self.epoch) << 22) | (self.datacenter_id << 17) | (self.machine_id << 12) | self.sequence
```

## Gotchas

- **Clock moving backward** (NTP correction, manual adjustment, VM pause/resume) breaks the "monotonic within a millisecond" assumption and can produce duplicate or out-of-order IDs. Generators typically raise or stall rather than risk a collision.
- **Limited epoch range**: a 41-bit timestamp only covers about 69 years from whatever epoch you pick, plan a migration path well before that window closes.
- **Fixed scaling ceiling**: datacenter/machine/sequence bit widths are baked into the format at design time. Outgrowing 32 datacenters, 32 machines per datacenter, or 4096 IDs/ms on one machine means changing the bit layout, not a config value.