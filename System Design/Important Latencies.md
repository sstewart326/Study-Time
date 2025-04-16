
|   |   |
|---|---|
|Component|Time (nanoseconds)|
|L1 cache reference|0.9|
|L2 cache reference|2.8|
|L3 cache reference|12.9|
|Main memory reference|100|
|Compress 1KB with Snzip|3,000 (3 microseconds)|
|Read 1 MB sequentially from memory|9,000 (9 microseconds)|
|Read 1 MB sequentially from SSD|200,000 (200 microseconds)|
|Round trip within same datacenter|500,000 (500 microseconds)|
|Read 1 MB sequentially from SSD with speed ~1GB/sec SSD|1,000,000 (1 milliseconds)|
|Disk seek|4,000,000 (4 milliseconds)|
|Read 1 MB sequentially from disk|2,000,000 (2 milliseconds)|
|Send packet SF->NYC|71,000,000 (71 milliseconds)|
- We know that a single server (with 64 cores) can handle 64000 RPS.