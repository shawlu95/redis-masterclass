## HyperLogLog

- has nothing to do with logging
- **approximate** count of unique element
- similar to a set, but doesn't store any element
- add element: `PFADD`
- check cardinality `PFCOUNT`
- 12kb no matter how many elements are added
- 0.81% hash collision

### When to use

- enforce each user can only contribute one view to each product
- less expensive to store user id in a set
