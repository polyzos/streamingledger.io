---
title: 'The Importance of Unified Batch and Streaming in Modern Data Processing.
'
date: 2024-09-12
permalink: /posts/unified-batch-and-streaming
tags:
  - unified batch and streaming
  - data architecture
---

Data lakes have revolutionized how we store and manage vast amounts of structured, semi-structured, and unstructured data for many years. 

However, a significant challenge has persisted: efficiently handling updates and merging data from multiple streams on the data lake. 

Traditionally, data lakes have been excellent for append-only operations, but they've struggled with handling updates, deletions, and merges - all of which are crucial for maintaining up-to-date, accurate datasets, especially in real-time analytics and dynamic use cases.

```java
DataStream<Tuple2<String, Double>> normalizedStream = userActions
        .map(action -> {
            // Extract and normalize features from the action
            double normalizedValue = normalize(action);
            return new Tuple2<>(action.getUserId(), normalizedValue);
        });

```


Next lets see some Flink SQL code.

```sql
CREATE TABLE anomaly_detection_results (
    deviceId STRING,
    timestamp BIGINT,
    features ARRAY<DOUBLE>,
    is_anomaly BOOLEAN
) WITH (
    'connector' = 'kafka',
    'topic' = 'anomaly-results',
    'properties.bootstrap.servers' = 'localhost:9092',
    'format' = 'json'
);
```