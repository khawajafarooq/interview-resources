* [Hadoop and Hama Deployment Guide](http://people.apache.org/~tjungblut/downloads/hamadocs/ApacheHamaInstallationGuide_06.pdf)
* 

### Questions asked during interview:
RDD vs Data Frames
How to put data on HDFS
Triggers in SQL
Star schema vs snow flakes
Count(car_name) join
What design patterns
TDD
Good developer
Your experience especially big data
Linux and Unix experience -> cp command


###General:

-> Q: 4 Vs:
Volume: 
Variety: Structured/unstructured
Velocity: Frequency of incoming data 
Veracity: Trustworthiness of data
Value:

http://www.dummies.com/how-to/content/the-4-vs-of-big-data.html


-> Q: Apache Kafka
Publish-scriber model
Produces -> topics -> consumers
Topic -> is a feed to which messages are published. Kafka maintains a partitioned log. 
Producers -> Publish data to the topic of their choice
Consumer -> 

Uses -> Website Activity Tracking, Stream Processing, Log Aggregation, Commit log

-> Q: Big data companies ? 
Hadoop Distributions: 
Cloudiera: Cloud Management Suite to automate installation process, reduce deployment time, displaying real time nodes. Layers of administrative and management capabilities
Horton works: All products are completely open source. Horton work data platform, contains most important components of hadoop eco system. Extensive testing, 
MapR: Replaces HDFS and has its own MapRFS. Enterprise grade features, reliability and easy of use. More production ready


-> Q: Comparisons between Hortonworks and Cloudera.
Both provide enterprise ready distributions. Cloudier is more towards properiotry softwares whereas hortonworks is focused towards open source. 

-> Q: Lambda Architecture
Hadoop can handle Volume (batch processing) but to handle handle Velocity we need a stream processing engine. Some times we need both systems and a combination of stream and batch is referred to as Lambda architecture

Batch Layer (MapReduce/Spark/Pig)
Speed Layer (Spark Streaming/ Storm)
Serving Layer

Technology agnostic, master data is immutable ( so even if the data gets corrupts we can go back)
- Maintaining 2 complex systems for Batch and Stream processing is very challenging
https://dzone.com/articles/lambda-architecture-big-data


###Apache Spark:
#####Spark EDX course:
Scalable, efficient analysis of Big Data

-> Big Data:
Click, Ad impression, Billing, watching a video, request to a server, transaction, messages. All of this can be recorded and analyzed.
Also comes from user generated content, Facebook, instagram, twitter, yelp
Health and scientific computing, Hadron collider peta bytes of data, protein application, genomics
Social graphs, graph data
Web server logs
System logs
Internet of things

-> RDD vs DataFrame vs Dataset
	
- **RDD: 1.0** slow because of serialization and sending structure and data to different nodes. Use RDDs when you donot want to impose a schema on data and your data is unstructured.
- **DataFrame: 1.3** .. added schema to avoid the serialization. Data is organized in columns. Developers can impose schema. Type safety is gone in this API.
- **DataSet 1.6:** can do sql style queries. Brings the best of both worlds. Has the serialization mechanism of DataFrame and type safety of RDDs. 
- http://www.agildata.com/apache-spark-rdd-vs-dataframe-vs-dataset/

![DataSet vs DataFrame](https://github.com/bsikander/interview-resources/blob/master/DataSet%20vs%20DataFrame.png)

![RDD vs DataFrame](https://github.com/bsikander/interview-resources/blob/master/RDD%20vs%20DataFrame.png)


-> Structure Specture:
Unstructured -> plain text, media
Semi-structured -> Documents, XML -> Maybe we can infer the type
Structured -> We know the type of data -> relational dos, 

In spark we have 2 ways how it knows about the schema
-> dynamically it can infer while reading a row
-> programmer stoically specifies it.

:: Only 20% of data is sturcuted
:: Spark works with Sturcutred/Semi-structured data but can also work with unstructured but after ETL process. So, we impose structure on unstructured data.
:: Problem with Big Data is that data is growing faster than computation speed 
:: Storage getting cheaper

FB Daily logs -> 60 TB
Google Web Index -> 10 PB
Youtube -> 1 PB everyday

-> Challenge is that one machine cannot store and process  all the data. 
  - Solution: Process on a cluster of machines.

We take data and partition is into multiple machines memory and perform analysis. DataFrame is responsible for this.
Spark is a computing framework. Provides programming abstraction and parallel runtime to hide complexities of fault tolerance and slow machines.

-> Spark Components:
Spark SQL, Spark Streaming, GraphX, MLLib and Core Apache Spark

-> Spark Program consists of Driver and Workers
Driver runs on 1 machine … 
worker runs on cluster or multiple threads on a local machine
Data frames are distributed in cluster
SparkContext is the first object created it tells spark how and where to access a cluster

Master parameter of SparkContext determines the type and size of cluster
local -> 1 worker thread
local[k] -> locally with k worker threads
spark://Host:Port -> runs on a cluster
mesos://Host:Port -> runs on a Mesos cluster


-> Data Frames:
Primary abstraction in spark
Once created they are immutable
You can construct a DF by transforming another DF or loading a data from hfs or file

2 types of operations on DF: Transformation and Actions
-> Transformation are lazy and only performed when Actions are performed
-> Can also persist DFs on disk or memory

-> Cycle
data -> DF ->transformation (select, filter) -> action

-> Spark Transformations:
Creates new DF from an existing DF
Lazy evaluation

Useful transformations -> filter, sort, orderby -> distinct -> explode 
Grouped Transformations -> groupby, agg, count, avg, 

-> Actions
Actions causes the transformation to executes to get results

show(n), take(n), collect (returns all of the data from all the cluster be careful) ,count, describe (works on numerical columsn) shows the avg, min, max, stddev etc

-> if you apply an action on a DF multiple times, then each time Spark will load the DF from memory and perform the action for each action specified in 
code. use DF.cache(), this will tell Spark to not recompute and use the cached value.


-> Where Spark program runs: At driver or executors or both ?
so, a=a+1 runs on driver
linesDF.filter(isComment) -> since DF is distributed and filter needs to be executed on each of them. it is ran on executors
linesDF.count() -> runs on both. First all counts is ran on DFs and then the result is combined on driver to compute the final result.


a = aDF.collect()
b = bDF.collect()
newDF=SparkContext.createNewDataFrame(a+b)

Now, first all the data (a and b) from all the machines is sent to the driver. Then we combine the data sets and generate a new DF and it distributed the data back to machines again. This is not a good implementation. So, use unionall. e.g a.unionAll(b). Runs only on executors.



-> Big data started way earlier but at time we were using a big box with many cores and memories. It was expensive and had its limits. Cloud computing changed everything. Now, we use cheap hardware to build clusters for big data processing but it has its own problems.

	-> Harddrives fail
	-> Network slower (latency) than sharing memory
	-> Uneven performance

-> What is hard about cluster computing ?
	-> divide work across cluster
	-> how to handle failure

-> Motiviation for Spark
	Map/Reduce phase read and write from harddrive and it is slow. 


——> Spark Job Executation:
The following happends when a Spark Job is triggered
	- Catalyst optimizer analyzes the unoptimized query plan and tries to optimize it.
	- Once it is optimized then multiple physical plans are created. 
	- It choses the most cost efficient physical plan 
	- Spark executes the job.

-> newDF.explain(True) can be used to examine the query plan.

-> What is an “RDD Lineage”?
  - The RDDs in Spark, depend on one or more other RDDs. The representation of dependencies in between RDDs is known as the lineage graph. Lineage graph information is used to compute each RDD on demand, so that whenever a part of persistent RDD is lost, the data that is lost can be recovered using the lineage graph information.
  
->  What is Spark Core?
  - It has all the basic functionalities of Spark, like - memory management, fault recovery, interacting with storage systems, scheduling tasks, etc.
  
-> What is the difference between persist() and cache()
  - persist () allows the user to specify the storage level whereas cache () uses the default storage level.
  - The various storage/persistence levels in Spark are -

    MEMORY_ONLY
    MEMORY_ONLY_SER
    MEMORY_AND_DISK
    MEMORY_AND_DISK_SER, DISK_ONLY
    OFF_HEAP

-> Does Apache Spark provide check pointing?
  - Lineage graphs are always useful to recover RDDs from a failure but this is generally time consuming if the RDDs have long lineage chains. Spark has an API for check pointing i.e. a REPLICATE flag to persist. However, the decision on which data to checkpoint - is decided by the user. Checkpoints are useful when the lineage graphs are long and have wide dependencies.
  
->  Explain about the core components of a distributed Spark application.

    Driver- The process that runs the main () method of the program to create RDDs and perform transformations and actions on them.
    Executor –The worker processes that run the individual tasks of a Spark job.
    Cluster Manager-A pluggable component in Spark, to launch Executors and Drivers. The cluster manager allows Spark to run on top of other external managers like Apache Mesos or YARN 
  
  

