#database #snowflake #ids #distributed-computed #postgresql
Snowflake IDs, or snowflakes, are a form of unique identifier used in distributed computing. The format was created by Twitter. Further details can be found [here](https://abheist.com/twitter-snowflake-for-unique-ids/)

In PostgreSQL you can generate Snowflake IDs via the following function:
``` sql
CREATE SEQUENCE PUBLIC.global_snowflake_id_sequence;

CREATE OR REPLACE FUNCTION PUBLIC.generate_snowflake_id(OUT result BIGINT) AS $$
DECLARE
    epoch bigint := 1314220021721;
    sequence_id bigint;
    milliseconds bigint;
    -- The id of this database shard, must be set differently, for each schema.
    shard_id int := 1;
BEGIN
    SELECT nextval('PUBLIC.global_snowflake_id_sequence') % 1024 INTO sequence_id;
    SELECT FLOOR(EXTRACT(EPOCH FROM clock_timestamp()) * 1000) INTO milliseconds;
    result := (milliseconds - epoch) << 23;
    result := result | (shard_id << 10);
    result := result | (sequence_id);
END;
$$ LANGUAGE PLPGSQL;
```