## Sorted Set

- scores have to be number, not string
- members are unique, scores don't have to be unique

### Common Command

- add member `ZADD`
- check member score `ZSCORE`
- remove `ZREM`
- cardinality `ZCARD`
- count members in score range `ZCOUNT` (inclusive both end)
  - `ZCOUNT products 0 55` means `0 <= score <= 55`
  - `ZCOUNT products (0 (55` means `0 < score < 55`
  - `ZCOUNT products -inf +inf`, `ZCOUNT products 50 +inf`
- pop the smallest `ZPOPMIN`
  - remove two smallest `ZPOPMIN products 2`
- pop the largest `ZPOPMAX`
- increment a score `ZINCRBY`, members will be re-sorted
- `ZRANGE` return members in a range of **index** (zero-based)
  - `ZRANGE products 1 2 WITHSCORES` return scorers too
  - `ZRANGE products 0 50 BYSCORE WITHSCORES` retrieve by score, not index (can use `(`, `)`, `inf`)
  - `ZRANGE products 1 2 REV` return with reversed sorting order, not the result order
  - `ZRANGE products 1 2 LIMIT 1 2` skip the first, return the next two

### Use Case

- want to sort a relationship; e.g. most recent k posts of a user (sorted by unix timestamp)
