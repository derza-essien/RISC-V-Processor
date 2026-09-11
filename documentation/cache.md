# Cache

The cahce is a smaller memory section which is used to store frequently used data, allowing for faster searching of data compared to main memory.

In terms of hardware resources, one way to look at this is to imagine the cache to be a memory block stored using distributed RAM, whereas main memory is stores as BRAM. Given that LUTRAM can be asynchronously read, whereas BRAM has a 1 (or 2) cycle read latency, LUTRAM can be used for smaller depth memory structures for faster access.

The cahce in this system has been implemented as **L1 2-way associative cache** with a **Least Recently Used, Write-Through system**.

Each entry into the cache contains a struct of the following signals.

```systemverilog
typedef struct packed {
        logic                   valid; // ensures valid data is inserted
        logic                   lru; // used for policy 
        logic [TAG_WIDTH-1:0]   tag; // used to match entries
        logic [DATA_WIDTH-1:0]  data;
    } cache_struct;
```

When we have a read request, we use the `tag` and `valid` signals to determine whether we have a match (i.e. the correct data is found). On a hit, we will swap the `lru` bit (which is high if way 1 is the least recently used way, and low for way 0).

If we have a cache miss, we enter a state machine which requires a search in main memory for the valid data. This calls a `cache_stall` signal which stalls the pipeline in the earlier stages for one cycle as we search main memory for the correct data.

On a write, if both ways have data currently, the way which is the least recently used is replaced.