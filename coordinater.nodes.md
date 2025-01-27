# Coordinator nodes in the ELK stack 

A coordinator node in an ELK (Elasticsearch, Logstash, Kibana) stack is a special node in Elasticsearch that serves as an intermediary for search and indexing requests. 
Its main task is to coordinate requests without storing or processing data itself. 
The tasks and application scenarios of a coordinator node are described in detail below. 

## Main tasks 

### 1. Process and distribute requests 
The Coordinator Node receives search requests and write requests from clients. 
It analyzes the request, divides it into smaller tasks and forwards them to the corresponding data nodes, which store the actual data. 

### 2. Aggregation of results 
For search queries, the coordinator node collects the partial results from various data nodes and aggregates them into an overall result that is returned to the client. 

### 3. Resource optimization 
There are no coordinator nodes own load for storage or processing, which means that they are used exclusively for the distribution and coordination of requests. 
This reduces the load on the cluster and requests can be processed more quickly. 

### 4. Load Balancing 
They distribute requests evenly across the entire cluster, preventing individual data nodes from becoming overloaded. 

### 5. No data storage 
Coordinator nodes do not have their own shards and do not store any data. This allows them to focus on processing requests and coordination. 

## Typical usage scenarios 

- Large clusters: In large Elasticsearch clusters with many data nodes, coordinator nodes help distribute the load efficiently. 
- Search query optimization: Improve response times for complex search queries by aggregating and coordinating results. 
- Decoupling of functions: You relieve the load on the data nodes, which then focus on data processing and storage can concentrate. 

## Configuration of a coordinator node

A Coordinator Node is specified through configuration by disabling all roles except the coordination role. 
In the elasticsearch.yml file this might look like this: 



```yaml
node.master: false
node.data: false
node.ingest: false
```

# The node then acts exclusively as a coordinator node.
