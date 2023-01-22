## Redis Hash

- set key val in alternating fashion: `HSET company name foo ceo bar` for `company: { name: foo, ceo: bar}`
- get a field: `HGET company ceo`
- get entire hash `HGETALL company`
- check if field exists `HEXISTS company ceo` _does not check truthiness of the value_
- delete a field `HDEL company ceo`
- increment a field by amount `HINCRBY company stock 100`
- example in [Basic_Hash.json](./rbook/Basic_Hash.json)

## When to Use Hash

- record has many attributes (e.g. users, items)
- a collection of these records have to be sorted in many different ways
- often need to access a single record at a time (e.g. session)

## When Not to Use Hash=

- record is only for counting or enforcing uniqueness (likes, views)
- record only stores one or two attributes
- used for creating relation beteween records
- record changes over time (bid price)
