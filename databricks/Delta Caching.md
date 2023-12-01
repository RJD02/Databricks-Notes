Delta is made of many components:
* Parquet data files organized or not as partitions
* JSON files as transaction log
* Checkpoint file

Spark has it's own caching features based on DataFrames and RDDs.
In spark, you can call cache() or persist() functions to tell the spark engine to cache data into the worker memory.

*Delta comes with 2 caching features, the **Delta Cache** and the **Result Cache*** 
<bold>Result cache is a feature of Delta Cache</bold>

# Delta Cache
It will keep local copies(files) of remote data on the worker nodes. Applied only on Parquet files(but delta is made of Parquet files)
Avoid remote reads during big workloads.
It uses local storage, we are able to configure the amount of storage dedicated for this cache and it's sub-sections:
`spark.databricks.io.cache.maxDiskUsage`: disk space per node reserved for cached data in bytes
`spark.databricks.io.cache.maxMetaDataCache`: disk space per node reserved for cached metadata in bytes
`spark.databricks.io.cache.compression.enabled`: should the cached data be stored in compressed format

# Result Cache
Provides the ability to cache a subset of data(query results)
If we need consistent performance on a specific query, this is it.
Once the query is cached, subsequent queries avoid reading files(as much as possible)
Result cache is automatically invalidated once the underlying files is updated or if the cluster is restarted.
