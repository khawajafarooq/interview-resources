* [Hadoop and Hama Deployment Guide](http://people.apache.org/~tjungblut/downloads/hamadocs/ApacheHamaInstallationGuide_06.pdf)
* 

###Apache Spark:
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
  
  

