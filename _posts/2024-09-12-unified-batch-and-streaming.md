---
title: 'The Importance of Unified Batch and Streaming in Modern Data Processing.
'
date: 2024-09-12
permalink: /posts/unified-batch-and-streaming
tags:
  - unified batch and streaming
  - data architecture
---

# The Importance of Unified Batch and Streaming in Modern Data Processing.

In the past decade, data-driven companies have evolved from processing periodic batches of data to needing real-time insights from continuous streams. However, the journey hasn’t been seamless.

Historically, companies have been forced to use two different technology stacks to handle batch and streaming workloads separately. This separation has resulted in a host of challenges, from increased operational complexity to delayed insights.

Today, we’re seeing a shift toward the unification of batch and streaming processing into a single stack. Unified data platforms offer the promise of managing both workloads seamlessly, reducing complexity and enabling real-time analytics at scale.

The following is a great presentation from Linkedin, exploring batch and streaming unification.

<iframe width="560" height="315" src="https://www.youtube.com/embed/ImXFxB5hXs0?si=lzHAAf2K14qvgTWv" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

In this article, we’ll explore why unifying batch and streaming is critical, what properties a modern unified data platform must have, and how it affects various layers of the data ecosystem — from ingestion and compute to storage and development.

## Separate Stacks for Batch and Streaming
Traditionally, organizations have employed two distinct architectures to process data, each tailored to specific needs:

### Batch Processing:
* Typically used for large-scale, periodic processing of data (e.g., nightly ETL jobs). 
* Systems like Apache Hadoop and later Apache Spark have been popular for running heavy batch workloads. 
* Latency is generally higher, ranging from hour to day level, depending on how frequently the batch jobs are triggered.

### Stream Processing:
* Designed for real-time or near-real-time processing, continuously consuming data from event streams (e.g., Apache Kafka). 
* Technologies like Apache Flink are widely used for low-latency, real-time analytics. 
* Latency is typically in milliseconds or seconds, providing up-to-the-moment insights. 

* The problem is that companies end up managing **two separate infrastructures** for ingesting, storing, and processing data. Data duplication often occurs, where the same data must be ingested and stored differently for batch and streaming pipelines, while operational overhead increases as teams maintain two technology stacks with different tools, frameworks, and performance trade-offs.

## The Importance of Unifying Batch and Streaming!
With the growing demand for real-time data insights alongside historical batch processing, many organizations now recognize the need for unified data processing platforms that can handle both batch and streaming workloads efficiently.

Key reasons why unifying these two paradigms is essential include:

**Operational Efficiency:** By converging batch and streaming, companies can reduce the complexity of managing separate infrastructures. This means fewer moving parts, less data duplication, and simplified operational management.

**Real-Time and Historical Data Processing:** organizations can access and process both real-time and historical data without needing to switch between systems. This provides a complete picture, leveraging both real-time analytics with historical trends for better decision-making.

**Consistency Across Workloads:** A unified platform ensures consistent processing models across both batch and streaming. This eliminates the discrepancies that arise from using different technologies with different data semantics, ensuring that data transformations applied to streams are also applied to historical data.

**Scalability and Flexibility:** Unified architectures are inherently more scalable because they are designed to handle varying workloads — whether it’s processing a large batch job or handling high-throughput streams of data. Organizations gain flexibility to adjust resource allocation dynamically based on current workloads.

**Cost-Effectiveness:** Maintaining two distinct systems leads to redundancy in terms of resources and infrastructure costs. Unifying batch and streaming on a single platform can significantly reduce infrastructure costs while optimizing resource usage.

## Key Properties of a Unified Data Stack
To support both batch and streaming workloads efficiently, a unified data stack must have specific characteristics across all layers of the data pipeline, from ingestion to storage and compute.

Next, let’s see the necessary properties of a unified platform and how it addresses both batch and streaming needs.

### Unified Data Ingestion Layer
The ingestion layer collects data from different sources — whether it’s event-driven data from Kafka, relational databases, or log files. In a unified architecture, this layer must:

* **Support both batch and streaming data sources:** Whether the data arrives as a continuous stream (e.g., via Kafka or Pulsar) or as periodic batches (e.g., from flat files or databases), the ingestion framework should handle both seamlessly. 
* **Seamless CDC Integration:** Change Data Capture (CDC) technology should be supported natively to keep the data lake synchronized with source systems in both real-time and batch scenarios. 
* **Latency Tolerance:** The ingestion framework should accommodate low-latency streaming while also supporting high-throughput batch ingestion, with the ability to switch between or combine these modes as needed. We refer to this functionality as snapshot and incremental data reading.

### Unified Compute Layer
The compute layer is where data is processed, transformed, and enriched. A unified compute framework must:

* **Handle both real-time and batch processing:** The compute engine must be capable of processing data in real-time streams and large-scale batch workloads using the same APIs and data models. 
* **Stateful Processing:** Real-time processing often requires maintaining state (e.g., tracking user sessions or windowed aggregations). The compute engine must manage the state efficiently in both streaming and batch contexts. 
* **Event-Time Semantics:** In streaming applications, the ability to process data based on the event time (when the event occurred) is crucial. Unified compute engines should maintain accurate event-time processing for both batch and streaming data. 
* **Exactly-Once Semantics:** To ensure data consistency, the compute engine should support exactly-once processing guarantees, which are critical for both real-time and batch pipelines. 

It also offers capabilities to support batch processing, like a hybrid shuffle mode, adaptive and speculative execution, operator fusion codegen and more

### Unified Storage Layer
The storage layer in a unified architecture needs to support data retention and retrieval in a way that accommodates both real-time and historical querying:

* **Transactional Support:** Data storage systems should provide ACID transactions to ensure that both batch and streaming updates are consistent and atomic, even when different workloads write to the same data store.
* **Efficient Querying:** The storage layer should support low-latency querying for real-time data while also being optimized for large-scale batch processing.
* **Schema Evolution and Flexibility:** Since both batch and streaming data may undergo schema changes, the storage system must support schema evolution without breaking existing queries or applications.
* **Time-Travel and Versioning:** To enable access to historical snapshots alongside real-time data, the storage layer should support time travel — the ability to query past versions of the data — while also maintaining efficient storage for real-time updates. 
* **Streaming reads/writes:** To enable real-time analytics, in addition to batch reads/writes, the storage needs to be able to support streaming read/writes. In addition, it also needs to support upserts efficiently as they are crucial for streaming data processing.

### Unified Development and API Layer
Another important aspect of a unified batch and streaming platform is the development experience. Engineers should be able to use the same development tools, languages, and APIs for both streaming and batch workloads:

* **Single API for Batch and Streaming:** A unified platform should offer a single API that allows developers to write code once and run it in both batch and streaming contexts without changes. 
* **Unified Data Models:** The data model for batch and streaming should be consistent, allowing data transformations, aggregations, and joins to work seamlessly across both paradigms. 
* **Extensibility and Integration:** The platform should integrate easily with the broader data ecosystem, supporting plugins for various sources, sinks, and connectors (e.g., JDBC, Kafka, S3).


## The Holy Grail Of Unified Batch and Stream Processing
**Apache Flink CDC**, **Apache Flink**, and **Apache Paimon** are a powerful trio, that enable organizations to unify batch and streaming architectures.


Apache Flink provides a unified API for both batch and streaming processing, which means users can run the same set of code whether it’s batch or stream.

Apache Flink CDC is a framework that provides snapshot and incremental data ingestion. It provides also a seamless experience for schema synchronization, full database synchronization, and new table discovery.

Apache Paimon is a modern lake storage layer that supports streaming reads/writes, and batch reads/writes. It also provides ACID transactions, time travel, and schema evolution, making them ideal for unified architectures that handle both batch and streaming.

Moreover, Flink 1.20 introduced the **Materialized Table**, for simplifying the development of batch and streaming applications. The engine can intelligently decide if it’s a batch, incremental, or stream processing job.

## Conclusion
As data needs continue to evolve, the separation between batch and streaming is becoming an unnecessary burden. Companies need both real-time insights and large-scale historical analysis in their data pipelines. By unifying batch and streaming into a single architecture, organizations can dramatically simplify their operations, reduce costs, and unlock new capabilities in real-time and historical analytics.

Apache Flink CDC, Apache Flink, and Apache Paimon combined with the Materialized Table help shape this unified future by providing the necessary infrastructure and capabilities to support both types of workloads.

Whether you’re processing massive batch ETL jobs or handling high-frequency event streams, a unified stack can offer a scalable, consistent, and efficient way to manage your data.

By consolidating batch and streaming into a cohesive stack, companies can gain the agility needed to adapt to modern data demands, providing real-time insights and large-scale historical analysis with minimal complexity.