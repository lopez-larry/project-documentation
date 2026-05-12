# Learning Apache Spark: Repository overview and step‑by‑step lesson plan

Apache Spark is a unified analytics engine for large‑scale data processing. The official documentation explains that Spark provides high‑level APIs in Java, Scala, Python and R, an optimized engine for executing general computation graphs, and a rich set of higher‑level tools including Spark SQL, pandas API on Spark, MLlib, GraphX and Structured Streaming. These modules correspond to major sub‑directories in the open‑source repository and form the foundation for learning Spark.
## 1 Repository directory map
The Spark repository is large because it contains modules for different languages (Scala/Java, Python and R), libraries for SQL, streaming, machine learning and graph processing, as well as build scripts and documentation. Understanding the purpose of the main directories will help you navigate the code base and know where to look when troubleshooting or contributing. The table below summarizes the most important top‑level directories (listed in the repository root) and what they contain.

| Directory                                                         | Purpose                                                                                                                                                                                                                                                                                          |
| ----------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **core/**                                                         | Core engine of Spark written in Scala/Java.  It implements the basic execution engine, scheduler, memory management and the original RDD API.  Other modules depend on this package.                                                                                                             |
| **sql/**                                                          | Spark SQL, DataFrame and Dataset implementation.  The documentation describes Spark SQL as a higher‑level tool for SQL and structured data processing.  This module includes the Catalyst query optimizer, logical/physical plans, DataFrame operations and Spark Connect server implementation. |
| **streaming/**                                                    | Legacy streaming API based on DStreams.  Provides functions for processing data streams in mini‑batches.  Structured Streaming (in `sql/`) is now the preferred interface, but the streaming module is retained for backward‑compatibility.                                                      |
| **mllib/** and **mllib‑local/**                                   | MLlib machine learning library (algorithms, feature transformers, pipeline APIs).  `mllib‑local` provides a local implementation for testing without Hadoop dependencies.                                                                                                                        |
| **graphx/**                                                       | GraphX for graph processing.  Includes APIs and algorithms for graph analytics.                                                                                                                                                                                                                  |
| **python/**                                                       | PySpark—the Python API for Spark.  Contains wrapper functions and Python implementations of the DataFrame API, streaming, MLlib, etc.  When you `pip install pyspark`, much of the code comes from this directory.                                                                               |
| **R/**                                                            | SparkR—R bindings for Spark (deprecated).                                                                                                                                                                                                                                                        |
| **examples/**                                                     | Example applications in Scala, Java, Python and R.  The `README.md` notes that sample programs are in the `examples/src/main` directory and can be run with `bin/run‑example`.  Exploring these examples is a great way to learn.                                                                |
| **bin/**                                                          | Executable shell scripts for users.  Important scripts include `spark‑shell` (interactive Scala shell), `pyspark` (interactive Python shell), `sparkR`, `spark‑submit` (submit jobs), and `run‑example`.  The README shows how to run these scripts to interactively use Spark.                  |
| **sbin/**                                                         | Administrative scripts for setting up a standalone cluster or launching master/worker daemons.                                                                                                                                                                                                   |
| **conf/**                                                         | Template configuration files.  Copy `spark‑env.sh.template` to `spark‑env.sh` and adjust environment variables; copy `spark‑defaults.conf.template` to configure defaults.  When using Hive, `hive‑site.xml`, `core‑site.xml` and `hdfs‑site.xml` should be placed in `conf/`.                   |
| **connector/**                                                    | Connectors for external data sources such as JDBC, Kafka, ORC, etc.                                                                                                                                                                                                                              |
| **hadoop‑cloud/**                                                 | Modules and integration tests for Hadoop cloud connectors (e.g., S3 via the Hadoop `fs.s3a` client).  Integration tests illustrate how to configure credentials using environment variables like `AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY`.                                                |
| **resource‑managers/**                                            | Support for different cluster managers (Standalone, YARN and Kubernetes).  Contains implementation classes, scripts and integration tests.                                                                                                                                                       |
| **assembly/**, **build/** and **project/**                        | Build‑related files for Maven and SBT.  `assembly` contains settings for packaging Spark distributions; `build` has Maven wrappers (`./build/mvn`); `project` holds SBT settings.                                                                                                                |
| **docs/**                                                         | Source for the documentation website.  Markdown files here (e.g., `docs/quick‑start.md`) are compiled into the official docs.                                                                                                                                                                    |
| **dev/**                                                          | Developer scripts used by Spark committers (e.g., running tests).  The README notes that tests can be run after building Spark using `./dev/run‑tests`.                                                                                                                                          |
| **common/**, **launcher/**, **data/** and other small directories | Shared utilities, the `spark‑launcher` API for embedding Spark, test data sets, UI integration tests, etc.  Exploring these is useful when contributing but not essential for learning to use Spark.                                                                                             |


## 2 Setting up Spark on your machine
### 2.1 Pre‑requisites
Spark runs on Windows, macOS and Linux. The official documentation states that Spark runs on any platform that has Java installed; it requires Java 17/21 and supports Python 3.10+ and R 3.5+. When using the Scala API, the application’s Scala version must match Spark’s build (Scala 2.13 since Spark 4.x). Ensure that the JAVA_HOME environment variable points to your Java installation or that java is on your system PATH.

### 2.2 Install PySpark via pip (recommended for Python learners)
- Install Python and Java (see prerequisites above).
- Install PySpark:
  - pip install pyspark 
- Start the interactive shell: run pyspark from a terminal. The Quick‑Start guide explains that if PySpark is installed via pip, you can start it by simply running pyspark. It will open an interactive Python session with a pre‑created SparkSession (spark variable). 
- Verify your environment:
```python 
>>> spark.range(1000 * 1000 * 1000).count()
# should return 1000000000
```

### 2.3 Download a pre‑built Spark distribution
If you prefer the Scala/Java shells or need the full distribution:
- Download: visit the downloads page on the project website and pick a package built for your Hadoop version or a “Hadoop‑free” package. 
- Extract the archive to a directory, for example ~/spark. 
- Run the shells:
  - Scala shell: ./bin/spark‑shell. 
  - Python shell: ./bin/pyspark. 
  - R shell (deprecated): ./bin/sparkR. 
  - Use the --master option to specify the deployment mode (e.g., --master local[2] to run locally on two threads).
- Run example programs: use the run‑example script. The README shows that running `./bin/run‑example SparkPi` executes the Pi example locally.

### 2.4 Build from source (for contributors)
  To build Spark yourself, you must have Apache Maven installed. The README instructs running

```bash
  ./build/mvn -DskipTests clean package
```

  which packages Spark and its example programs. After building, you can run the same scripts and examples as above.
## 3. Working with Spark interactively
  Spark’s shells make it easy to explore APIs and perform ad‑hoc data analysis. The Quick‑Start guide walks through creating DataFrames and performing transformations. Here is a condensed workflow:
  - Start a shell: run pyspark (Python) or spark‑shell (Scala). A SparkSession is available as spark.
  - Create a DataFrame from a text file (example uses the repository’s README.md):
```python 
textFile = spark.read.text("README.md")
textFile.count()   # returns number of rows:contentReference[oaicite:19]{index=19}
  textFile.first()   # shows the first row:contentReference[oaicite:20]{index=20}
 ```
  - Transformations and actions: use DataFrame/DataSet operations such as filter, select, groupBy and agg. For example:
  
```python
linesWithSpark = textFile.filter(textFile.value.contains("Spark"))
linesWithSpark.count()
```
  - Structured APIs: In Scala, you can use strongly‑typed Dataset[String] operations such as map, filter and reduce.
  
  - Exploring the examples under examples/src/main provides more sophisticated programs for word count, Spark SQL, machine learning pipelines, graph algorithms and streaming.
## 4 Connecting to major data sources
  Spark’s DataFrame API has built‑in support for many data sources. You choose a format (e.g., csv, parquet, json, jdbc) and specify options. 

### 4.1 File systems (local, HDFS and cloud storage)
  You can read and write files stored on the local file system or on Hadoop Distributed File System (HDFS) by specifying the appropriate path. For example:
``` python
# read a CSV file from the local filesystem
df = spark.read.format("csv").option("header", True).load("/path/to/file.csv")

# read a Parquet file from HDFS
parquetDF = spark.read.parquet("hdfs://namenode:8020/path/to/data.parquet")
```

To access Amazon S3 or other cloud object stores, Spark relies on Hadoop connectors (hadoop‑aws or hadoop‑azure). In the hadoop‑cloud module, integration tests illustrate that credentials are passed via environment variables such as AWS_ACCESS_KEY_ID and AWS_SECRET_ACCESS_KEY when running integration tests. In your own applications you set Hadoop configuration keys on the Spark session, for example:

```python
spark = (SparkSession.builder
         .appName("S3 example")
         .config("spark.hadoop.fs.s3a.access.key", "<access_key>")
         .config("spark.hadoop.fs.s3a.secret.key", "<secret_key>")
         .config("spark.hadoop.fs.s3a.endpoint", "s3.amazonaws.com")
         .getOrCreate())

df = spark.read.parquet("s3a://my-bucket/path/to/data.parquet")
```

### 4.2 JDBC databases
Spark SQL includes a JDBC data source that can read from and write to relational databases. The documentation notes that this approach returns results as DataFrames and is easier to use than the older JdbcRDD. To connect:
- Add the JDBC driver to the classpath. For example, to connect to PostgreSQL in the Scala shell you can run

```python 
./bin/spark-shell --driver-class-path postgresql-<version>.jar --jars postgresql-<version>.jar:contentReference[oaicite:25]{index=25}
```

- Use the JDBC data source:
```python 
jdbcDF = (spark.read
          .format("jdbc")
          .option("url", "jdbc:postgresql://host:5432/db")
          .option("dbtable", "schema.table")
          .option("user", "username")
          .option("password", "password")
          .load())

# perform transformations and then write back
jdbcDF.write.format("jdbc").option("url", ...).option("dbtable", "dest_table").save()
```

Refer to the JDBC data source documentation for options such as partitionColumn, numPartitions and custom queries.

### 4.3 Hive and the metastore
Spark can read and write Hive tables. Because Hive has many dependencies, they are not included in the default Spark distribution; if Hive dependencies are on the classpath, Spark loads them automatically. To use Hive:

- Place `hive‑site.xml`, `core‑site.xml` and `hdfs‑site.xml` into the `conf/` directory.

- Build a SparkSession with Hive support:

```python
from pyspark.sql import SparkSession
warehouse_location = "/path/to/spark-warehouse"
spark = (SparkSession.builder
          .appName("Hive Example")
          .config("spark.sql.warehouse.dir", warehouse_location)
          .enableHiveSupport()  # enables Hive metastore and UDFs:contentReference[oaicite:29]{index=29}
          .getOrCreate())
```
- Create or read tables using HiveQL:

```python
spark.sql("CREATE TABLE IF NOT EXISTS src (key INT, value STRING) USING hive"):contentReference[oaicite:30]{index=30}
spark.sql("LOAD DATA LOCAL INPATH '/path/to/kv1.txt' INTO TABLE src"):contentReference[oaicite:31]{index=31}
result = spark.sql("SELECT key, value FROM src WHERE key < 10 ORDER BY key")
result.show()
```
Spark will create a local metastore if one is not configured. spark.sql.warehouse.dir defines where managed tables are stored; hive.metastore.warehouse.dir is deprecated.

### 4.4 Structured Streaming
Although beyond basic installation, it is worth noting that Structured Streaming (located in sql/) allows processing streams of data as unbounded tables. This module inherits the optimizations and declarative API of DataFrames. The Spark programming guide includes examples for reading streams from Kafka, files or sockets and writing streaming queries to sinks (console, files, Kafka, JDBC, etc.).

## 5 Lesson plan for learning Spark
The following lesson plan provides a structured path to become proficient with Apache Spark. Adjust the pacing based on your background in distributed systems and programming.

- Week 1: Foundations and repository familiarization
  - Read the overview of Spark to understand its purpose and ecosystem. Learn the high‑level modules: SQL, streaming, MLlib, GraphX, pandas API.
  - Explore the repository using the directory map above. Skim through core/, sql/, python/, examples/ and 
   docs/quick‑start.md to see how Spark is organized.
  - Install Spark locally via pip install pyspark or download a pre‑built package and run the interactive shell.
  - Run simple commands in the shell. Use spark.range(...).count() to verify your installation.

- Week 2: DataFrames, Datasets and Spark SQL
  - Create DataFrames from local files and perform basic actions (count(), first()).
  - Learn transformations such as filter, select, groupBy and agg.
  - Use Spark SQL: register temporary views and write SQL queries. Examine the execution plans with explain().
  - Understand schema evolution and file formats: read/write CSV, JSON, Parquet and ORC. Use spark.read.format("parquet").load(...) and .write.format(...) to save results.

- Week 3: Advanced APIs and integration
  - Structured Streaming: read streaming data (e.g., from a socket or Kafka) and perform aggregations. Understand triggers and checkpoints.
  - MLlib: build machine‑learning pipelines. Explore algorithms for classification, regression and clustering.
  - GraphX: run graph algorithms like PageRank or Connected Components.
  - Spark Connect: learn about the client/server architecture introduced in Spark 3.4 (optional). It allows remote connectivity from any application.

- Week 4: Data source connectors and deployment
  - JDBC integration: connect to a relational database, load a table into Spark and write the results back. Experiment with partitioning options to parallelize reads.
  - Hive integration: configure hive‑site.xml and enable Hive support in SparkSession. Create tables and perform queries.
  - Cloud storage: configure Hadoop credentials to read/write from S3 or other object stores.
  - Deploying Spark: experiment with running Spark applications in cluster mode. Start with standalone mode using sbin/start‑master.sh and sbin/start‑worker.sh, then explore YARN and Kubernetes.

- Week 5 and beyond: Internals and contributions
  - Read deeper into the code. Study the Catalyst optimizer in sql/ and scheduler internals in core/.
  - Contribute: follow the contribution guide and learn how to build Spark with Maven and run tests using ./dev/run‑tests.
  - Stay up to date: follow Spark’s mailing lists and release notes; the project evolves quickly and new features such as Spark Connect may change workflows.

## Conclusion
  By exploring the repository structure, installing Spark locally, practicing with the interactive shells and examples, and connecting to common data sources, you will gain a solid foundation in Apache Spark. Use the lesson plan to guide your progression from basic DataFrame operations to advanced streaming and machine‑learning tasks. Remember to consult the official documentation for additional details and updates.