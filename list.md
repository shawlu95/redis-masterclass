## List

- lists are not array
- implemented as doubly linked list
- try not to use list (bad performance)

### Command

- get data:
  - `LINDEX` get element by index, negative index start from right
  - `LLEN` list length
  - `LPOS` provide a value and get the index
    - `LPOS temps 26` return null if not found
    - `LPOS temps 26 RANK 2` get the second instance of 26
    - `LPOS temps 26 COUNT 2` get first two occurences' index
    - `LPOS temps 26 MAXLEN 10` only search among the first 10 elements
    - see also `RPOS`
  - `LRANGE` gets a range of element by index, same as Python
    - `LRANGE 0 -1` get entire list
- add data
  - `LPUSH` head of linked list
  - `RPUSH` tail of linked list
  - `LPOP` remove first element from left, see also `RPOP`
  - `LPOP temps 2` remove 2 elements from left
- update data
  - `LSET temps 0 100` set first element to 100
  - `LTRIM temps 2 5` remove elements out side of index range 2~5
  - `LINSERT temps 30 15` insert 15 before 30
  - `LREM temps -2 25` from right to left, remvoe two copies of 25

### Use Case

- append-only or prepend-only data (temperature, stock price)
- only need the first/last N values
- no sort attribute, only by the order of insertion
- no filter criteria
- get title of most recently reviewed books
- can append timestmap and other info to the element, but losing the ability to join

```
DEL reviews
RPUSH reviews b2
RPUSH reviews a1
HSET books:a1 title 'good book'
HSET books:b2 title 'bad book'
SORT reviews BY nosort
  GET books:*->title
```
