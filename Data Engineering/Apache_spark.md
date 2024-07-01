
# Apache Spark Interview Questions

## Source: Data Savvy (YouTube)

### Q1. RDD vs DataFrame vs Datasets

**Answer:**
- **RDD (Resilient Distributed Dataset)**: The fundamental data structure of Spark, RDDs are immutable, distributed collections of objects that can be processed in parallel. They support two types of operations: transformations (e.g., map, filter) and actions (e.g., count, collect). RDDs are type-safe but can be less efficient due to a lack of optimization.
- **DataFrame**: A distributed collection of data organized into named columns, similar to a table in a relational database. DataFrames provide a higher-level abstraction than RDDs and use Catalyst optimizer for optimization, resulting in better performance. They are not type-safe.
- **Dataset**: A combination of RDDs and DataFrames, Datasets provide the best of both worlds with the ability to apply functional programming operations and the optimization benefits of DataFrames. Datasets are type-safe and use Catalyst for optimization.

### Q2. Repartition vs Coalesce

**Answer:**
- **Repartition**: Increases or decreases the number of partitions in a DataFrame or RDD. It involves a full shuffle of data across the network, making it an expensive operation. It is useful for increasing parallelism.
- **Coalesce**: Reduces the number of partitions without a full shuffle. It combines data from multiple partitions into fewer partitions, which is more efficient than repartitioning. It reduces the number of partitions, especially after filtering operations.

### Q3. Partition vs Bucketing

**Answer:**
- **Partitioning**: Divides data into distinct parts based on a column value. Each partition is a sub-directory in the file system. Partitioning helps in efficient data retrieval but can lead to small file problems if not managed properly.
- **Bucketing**: Organizes data into fixed-size parts based on a hash function of a column. Bucketing can help with query performance by reducing the amount of data to scan. Bucketing in Spark differs from Hive as it involves additional sorting within each bucket.

**When to use:**
- **Partitioning**: When queries frequently filter on a specific column, partitioning can improve query performance.
- **Bucketing**: When there are frequent joins on a specific column, bucketing can improve join performance.

**Small file problem**: Occurs when partitioning leads to many small files, which can degrade performance due to the overhead of managing numerous files.

**Bucketing in Hive vs Spark**: [Watch Video](https://youtu.be/Kr_AAkzGZsI?si=FATqBoNNaP3Cql8f&t=324)

**Size of each bucket**: Total data size / 128MB (128MB is the default data block size for HDFS).

### Q4. Avro vs Parquet

**Answer:**
- **Avro**: A row-based storage format suitable for write-heavy operations. It is compact, fast, and supports schema evolution.
- **Parquet**: A columnar storage format suitable for read-heavy operations. It is efficient for querying large datasets as it can skip unnecessary columns and supports efficient compression.

### Q5. Executor vs Executor Core

**Answer:**
- **Executor**: A JVM process launched on a worker node, responsible for executing a subset of tasks in a Spark job. Executors manage memory and perform computations.
- **Executor Core**: The thread running within an executor. It performs tasks such as data processing, computation, and task execution.

### Q6. Static Pruning, Dynamic Partition Pruning, Spark Performance Tuning

**Answer:**
- **Static Pruning**: Filters data at the DataFrame level before execution.
- **Dynamic Partition Pruning**: Optimizes join queries by dynamically pruning partitions during query execution.
- **Spark Performance Tuning**: Techniques include adjusting parallelism, optimizing joins, caching intermediate results, and avoiding shuffles.

**Threshold size limit for broadcast join**: Default is 10MB, configurable with `spark.sql.autoBroadcastJoinThreshold`.

### Q7. 10 Ways to Tune Spark Performance

**Answer:**
1. **TreeReduce or TreeAggregate**: Reduces network traffic by combining intermediate results in a tree structure.
2. **Kryo Serialization**: More efficient serialization library than Java serialization, reducing the time and space required for serializing objects.
3. **Caching**: Persisting intermediate data to speed up iterative computations.
4. **Optimizing Data Storage Formats**: Using efficient file formats like Parquet or ORC.
5. **Adjusting Parallelism**: Setting appropriate values for the number of partitions.
6. **Broadcast Joins**: Using broadcast variables for small tables to avoid shuffles.
7. **Data Skew Mitigation**: Distributing data more evenly across partitions.
8. **Avoiding Wide Transformations**: Minimizing operations like `groupBy` and `join` that cause shuffling.
9. **Specifying Resource Allocations**: Allocating the right amount of memory and cores.
10. **Using Catalyst Optimizer**: Leveraging Spark SQL’s query optimization.

### Q8. Spark Executor Tuning, Deciding Number of Executors

**Answer:**
- **Executor Tuning**: Involves configuring the number of executors, memory per executor, and cores per executor based on the cluster size and workload.
- **Deciding Number of Executors**: Depends on the total available resources, job characteristics, and desired parallelism. A typical approach is to set the number of executors such that each executor can process a reasonable amount of data without overwhelming the JVM heap space.

### Q9. Spark Lineage vs DAG

**Answer:**
- **Lineage**: The sequence of transformations applied to the original RDD. Lineage information is used for fault recovery.
- **DAG (Directed Acyclic Graph)**: Represents a series of computations in Spark. Each node is an RDD, and edges are transformations. DAG visualization helps understand job execution and optimization.

### Q10. Why Spark Dataset is Type Safe

**Answer:**
- **Type Safety**: Ensures that operations on Datasets are checked at compile-time, reducing runtime errors and providing better optimization through Catalyst.

### Q11. Spark Broadcast Variables

**Answer:**
- **Broadcast Variables**: Allow efficient distribution of large read-only data across all nodes, avoiding data transfer for each task.

### Q12. What is Spark Execution Model?

**Answer:**
- **Execution Model**: Spark jobs are divided into stages based on shuffle boundaries. Each stage consists of tasks executed in parallel. The driver coordinates task execution and collects results.

### Q13. What is the Role of SparkContext?

**Answer:**
- **SparkContext**: The entry point to Spark functionality. It initializes the Spark application, sets configurations, and connects to the cluster manager.

### Q14. Difference Between Client and Cluster Mode

**Answer:**
- **Client Mode**: The driver runs on the client machine submitting the application.
- **Cluster Mode**: The driver runs on one of the worker nodes within the cluster.

### Q15. What is Partition Skew, Reasons for It, and How to Solve It?

**Answer:**
- **Partition Skew**: Occurs when data is unevenly distributed across partitions, leading to performance bottlenecks.
- **Reasons**: Skewed data distribution, poor partitioning strategy.
- **Solutions**: Custom partitioning, salting keys, increasing parallelism, and using skew-aware joins.

### Q16. What is a Broadcast Join in Apache Spark?

**Answer:**
- **Broadcast Join**: A join strategy where a small DataFrame is broadcast to all executors to avoid shuffles. Suitable for joining a large DataFrame with a small DataFrame.

### Q17. What is the Difference Between Partition and Bucketing?

**Answer:**
- **Partition**: Divides data based on column values.
- **Bucketing**: Divides data based on a hash function and organizes it into fixed-size buckets.

### Q18. What are Different Types of Joins in Spark?

**Answer:**
- **Inner Join**: Returns rows with matching keys in both DataFrames.
- **Outer Join (Left, Right, Full)**: Returns rows with matching keys and includes unmatched rows from one or both sides.
- **Cross Join**: Returns the Cartesian product of two DataFrames.
- **Semi Join**: Returns rows from the left DataFrame that have matching keys in the right DataFrame.
- **Anti Join**: Returns rows from the left DataFrame that do not have matching keys in the right DataFrame.

### Q19. Why `count` When Used with `groupBy` is a Transformation Else It's an Action?

**Answer:**
- **Transformation**: When used with `groupBy`, `count` creates a new DataFrame with group-wise counts.
- **Action**: `count` as an action computes the total number of rows and triggers execution.

### Q20. If Your Spark Job is Running Slow, How Would You Approach to Debug It?

**Answer:**
- Check the DAG visualization for bottlenecks.
- Monitor resource usage (CPU, memory).
- Look for skewed partitions.
- Adjust parallelism and resource allocation.
- Review the job logs for errors or warnings.
- Optimize data storage and serialization formats.

### Q21. Difference Between Managed Table & External Table. When to Use External Tables?

**Answer:**
- **Managed Table**: Spark manages both the metadata and the data. Dropping the table deletes the data.
- **External Table**: Spark manages only the metadata. Dropping

 the table does not delete the data.
- **When to Use**: Use external tables when data needs to be shared across different applications or when you want to maintain control over the data lifecycle.

### Q22. Why We Are Not Using MapReduce These Days. Similarities Between Spark and MapReduce.

**Answer:**
- **Not Using MapReduce**: Spark provides faster performance due to in-memory processing, simpler APIs, and a unified engine for batch, streaming, and interactive analytics.
- **Similarities**: Both are distributed data processing frameworks, use distributed storage systems (like HDFS), and support parallel processing and fault tolerance.

### Q23. How Do You Handle Your PySpark Code Deployment? Explain About the CICD Process.

**Answer:**
- **Deployment**: Use tools like Docker, Jenkins, and Kubernetes for continuous integration and deployment. Version control with Git, automated testing, and monitoring are integral parts of the CICD pipeline.

### Q24. Have You Used Caching in Your Project? When & Where Do You Consider Using It?

**Answer:**
- **Caching**: Used to persist intermediate data in memory for faster access in iterative algorithms or when multiple actions are performed on the same data. Use caching when data is accessed repeatedly and fits into memory.

### Q25. How to Estimate the Amount of Resources for Your Spark Job?

**Answer:**
- **Estimation**: Based on data size, complexity of transformations, and job characteristics. Use the formula: 
  ```
  Number of Executors = Total Executors Memory / Executor Memory
  Number of Cores = Total Available Cores / Executor Cores
  ```
  Consider memory overhead, shuffle partitions, and data locality.

### Q26. Difference Between Narrow and Wide Transformation

**Answer:**
- **Narrow Transformation**: Operations like `map`, and `filter`, where each input partition contributes to only one output partition. No shuffle.
- **Wide Transformation**: Operations like `groupByKey`, and `join`, where input partitions contribute to multiple output partitions. Causes shuffle.

### Q27. Difference Between DataFrame and Dataset

**Answer:**
- **DataFrame**: Distributed collection of data organized into named columns, not type-safe.
- **Dataset**: Extension of DataFrame, provides type-safety and object-oriented programming interface.

### Q28. If Some Job Failed with Out of Memory Error in Production, What Will Be Your Approach to Debug That?

**Answer:**
- Check for memory-intensive operations.
- Increase executor memory.
- Optimize shuffles and joins.
- Persist intermediate data using disk storage.
- Review the job's memory usage and adjust configurations.

### Q29. What is DAG & How That Helps?

**Answer:**
- **DAG (Directed Acyclic Graph)**: Represents the sequence of computations. Each node is an RDD, and edges are transformations. Helps in understanding job execution, optimization, and fault tolerance.

### Q30. Which Version Control Do You Use?

**Answer:**
- Common version control systems: Git, SVN. Git is widely used for its distributed nature, branching capabilities, and integration with CICD tools.

### Q31. How Do You Test Your Spark Code?

**Answer:**
- Use unit testing frameworks like `pytest`, `unittest`, and libraries like `pyspark.sql.testing`.
- Mocking data sources and using small datasets for integration testing.
- Validate performance and correctness with end-to-end tests.

### Q32. What is Shuffling, Why Should We Minimize It?

**Answer:**
- **Shuffling**: The process of redistributing data across the cluster, often due to wide transformations. It involves disk I/O, network I/O, and serialization.
- **Minimizing Shuffling**: Reduces the overhead, improves performance, and avoids bottlenecks.

### Q33. If 199/200 Partitions are Getting Executed but After 1 Hour You Are Getting Error. What Things Will You Do?

**Answer:**
- Check for skewed partitions.
- Investigate resource exhaustion or hardware failures.
- Increase the number of retries (`spark.task.maxFailures`).
- Optimize the problematic partition by repartitioning or using different algorithms.
- Review logs for specific errors and bottlenecks.
