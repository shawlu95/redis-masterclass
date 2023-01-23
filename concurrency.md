## Concurrency

- use atomic update command without reading; e.g. `HINCRBY`, `HSETNX`
- use `watch` a key with transaction; if the key changed, all concurrent transactions fail
  - a new connection is created for the transaction, and closed once transaction is completed
  - watch the key before retrieving it from Redis
  - increase Redis round trip, doesn't scale well
  - first come first serve, but we may want the best, not the first (e.g. highest bidder)
- use lock, manually maintained
  - set a key such as `SET lock:item:a1 foo NX` tied to the locked key which only returns 1 if not set
  - process that successfully set the key can write to the locked key
  - once the process finishes, delete the lock key
  - other processes can claim the key as they try in quick succession
  - this is **not the redlock algorithm**, for production system, use **redlock** instead
  - see redlock: https://redis.io/docs/manual/patterns/distributed-locks/
  - corner case, if process fail, must release the lock with `PX` or catch block
  - corner case, if using `PX`, a long-hanging process may complete after lock expired, and delete the lock acquired by another process.
    - cannot be resolved by checking token value before deleting
    - use LUA script instead. When Redis executes LUA script, it won't be interrupted by any other process. It will execute from start to finish
- write LUA script

![alt-text](./asset/watch.png)

![alt-text](./asset/transaction.png)
