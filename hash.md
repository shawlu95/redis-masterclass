## Redis Hash

- set key val in alternating fashion: `HSET company name foo ceo bar` for `company: { name: foo, ceo: bar}`
- get a field: `HGET company ceo`
- get entire hash `HGETALL company`
- check if field exists `HEXISTS company ceo` _does not check truthiness of the value_
- delete a field `HDEL company ceo`
- increment a field by amount `HINCRBY company stock 100`
- example in [Basic_Hash.json](./rbook/Basic_Hash.json)
