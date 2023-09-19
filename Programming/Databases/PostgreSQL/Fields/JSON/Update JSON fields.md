#postgresql #json #jsonb #update #database
To update JSON/JSONB fields in a PostgreSQL database, without losing the existing data, execute the bellow query:
``` sql
UPDATE <table>
SET <json_field> = jsonb_set(<json_field>, '{<json_field_1_to_traverse>,<json_field_2_to_traverse>,<...>,<json_field_to_update_or_add>}','"<value_to_update_or_add>"')
WHERE <condition>;
```
