## Set Operation

- add `SADD`
- remove `SREM`
- union `SUNION`, `SUNIONSTORE`
- intersection `SINTER`, `SINTERSTORE`
- differnce `SDIFF`, `SDIFFSTORE`
- return all members `SMEMBERS`
- paginate all members `SSCAN`
- get a ramdom `SRANDMEMBER`
- pop a random `SPOP`
- cardinality `SCARD`

### When to use Set

- enforcing uniqueness, e.g. username
- relationship between entity, e.g. what items a user has liked `users#45:likes`
  - number of items liked `SCARD users#45:likes`
  - does user 45 like product 123: `SISMEMBER users#45:likes 123`
- find common attributes: `SINTER users#45:likes users#46:likes`
- maintain a blacklist, where ordere doesn't matter
