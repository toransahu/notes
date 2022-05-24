# Big Data

[TOC]

- batch vs stream processing
	- diff
		- batch
			- processing happens of blocks of data that have already been stored over a period of time
			- works well in situations where you don’t need real-time analytics results
			- when it is more important to process large volumes of data to get more detailed insights than it is to get fast analytics results
			- datasets typically looks-like:
				- bounded: batch datasets represent a finite collection of data
    			- persistent: data is almost always backed by some type of permanent storage
    			- large: batch operations are often the only option for processing extremely large sets of data

		- stream
			- if we want analytics results in real time
			- allows us to process data in real time as they arrive and quickly detect conditions within small time period from the point of receiving the data
			-  allows us to feed data into analytics tools as soon as they get generated and get instant analytics results
			- datasets typically are:
				- unbounded
				- The total dataset is only defined as the amount of data that has entered the system so far
				- The working dataset is perhaps more relevant, and is limited to a single item at a time
    			- Processing is event-based and does not “end” until explicitly stopped. Results are immediately available and will be continually updated as new data arrives
    		- Stream processing systems can handle a nearly unlimited amount of data, but they only process one (true stream processing) or very few (micro-batch processing) items at a time
    		- stream processing framework/engine category
				- Compositional Engines
					- developers define the Directed Acyclic Graph (DAG) in advance and then process the data
					- e.g. Samza, Apex and Apache Storm
				- Declarative Engines
					- Developers use declarative engines to chain stream processing functions. The engine calculates the DAG as it ingests the data. Developers can specify the DAG explicitly in their code, and the engine optimizes it on the fly.
					- e.g. Apache Spark and Flink
				- Fully Managed Self-Service Engines
					- A new category of stream processing engines is emerging, which not only manages the DAG but offers an end-to-end solution including ingestion of streaming data into storage infrastructure, organizing the data and facilitating streaming analytics.
					- e.g. Upsolver 	 


	- examples
		- batch
			- common
				- processing all the transaction at the end of day/week/month for various analysis
					- https://miro.medium.com/max/622/1*DZFsgsjpZw3P0dNzUAYjgg.png
			- google
				-
			- amazon
				-
			- project
				- Access Point log mining for analytics
		- stream 
			- common
				- order status in online transaction/shopping
			- google
				- google doc collaborative editing
				- google map location service
			- amazon
				-
			- project
				- Access Point live stats
				- Org/Site/Access Point/Client level events
				- Anomaly detection

	- frameworks
		- Hadoop MapReduce
			- Data Processing: batch only
			- Category: data processing engine

			- Fault-tolerance: uses replication for fault tolerance
			- Scalability: scalable upto 1000 nodes in single Cluster
			- Latency / Processing Speed: slow due to I/O disk (HDFS filesystem based) latency

			- Cost: less due to disk usages
			- Compatibility: compatible with all the data sources and file formats
			- Security: more secure due to codebase maturity
			- Scheduler: by external schedulers
			- Ease of Use: low-level APIs -> more codes to write; complex debugging
			- Duplicate Elimination: do not support

			- License: Apache open-source software (OSS)
			- Language Support: Java, C/C++, Ruby, Python, Perl, and Groovy
			- Machine Learning: no inbuilt APIs; compatible with Apache Mahout
		- Apache Flink
			- batch + stream
		- Apache Spark
			- Data Processing: batch + stream (in-memory batch data processing framework and supports stream processing by micro-batching)
			- Category: data analytics engine

			- Fault-tolerance: uses RDD and other data storage models for fault tolerance
			- Scalability: scalable upto 1000 nodes in single Cluster
			- Latency / Processing Speed: very fast in memory; fast while running on disk

			- Cost: more due to more RAM
			- Compatibility: compatible with all the data sources and file formats
			- Security: getting mature --> getting more secure
			- Scheduler: have own schedulers
			- Ease of Use: rich APIs -> easy to write code; easy to debug
			- Duplicate Elimination: capable; process every records exactly once

			- License: Apache open-source software (oss)
			- Language Support: Java, Scala, Python, and R
			- Machine Learning: inbuilt APIs

			- cluster computing technology framework
			- designed for fast computation on large-scale data processing
			- features SQL queries, Graph Processing, and Machine Learning
			- cluster manager options - Apache YARN, Mesos
			- resource manager option - Hadoop Distributed File System (HDFS), Google cloud storage, Amazon S3, Microsoft Azure
		- Apache Storm
			- ‘Hadoop of real time’
			- high throughput, low latency system
			- guarantees at least once processing of messages
			- best option for pure stream processing (need to tryout Flink)

			- Data Processing: stream (BackType --> Twitter --> analyze impact of businesses on social media)
			- Category: tbd

			- Fault-tolerance: tbd
			- Scalability: tbd
			- Latency / Processing Speed: tbd

			- Cost: tbd
			- Compatibility: tbd
			- Security: tbd
			- Scheduler: htbd
			- Ease of Use: tbd
			- Duplicate Elimination: tbd

			- License: Apache open-source software (oss)
			- Language Support: tbd
			- Machine Learning: tbd

		- Apache Samza
		- Apache Apex
		- AWS Kinesis
		- Azure Stream Analytics
		- Microsoft TPL Dataflow
		- Confluent KSQL
	- frameworks comparision
	- databases
		- ES
		- Cassandra
	- message queues
		- Kafka
			- is a distributed messaging platform based on the publish/subscribe model that was developed by LinkedIn (while monolithic--> microservice to communicate stream data between services)
		- Redis PubSub
		- Google Cloud Pub/Sub

# File Formats

## CSV

## parquet 

- https://parquet.apache.org/docs/
- https://github.com/apache/parquet-mr
- https://databricks.com/glossary/what-is-parquet
- https://db-blog.web.cern.ch/blog/zbigniew-baranowski/2017-01-performance-comparison-different-file-formats-and-storage-engines

## OCR

## avro
