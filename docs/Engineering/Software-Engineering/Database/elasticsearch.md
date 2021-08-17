# ElasticSearch

_- Shay Banon, 2010_

<h3>Table of Contents</h3>
[TOC]


# What

- ElasticSearch (ES) is a search and analytic engine (more than a No-SQL database)
- based on Apache Lucene library
- provides
    - distributed 
    - multi-tenant capable
    - full-text search engine
- through
    - HTTP web interface
    - and (schema-free) JSON documents
- kind: index & document based

# How
How does ElasticSearch work?

- ES uses a concept/data structure called Inverted Index
    - which is designed to perform very fast full-text search
- A document (says string/sentence) saved as well as is analyzed and tokenized for better search results
    - the sentance, say "this is a test string" is split into words, n-grams
    - and each part is mapped to relevant document id, position, and number of occurrences

- ES index is made up of one or more shards
- each shard can have zero or more replicas
    - these are individual Lucene indices
- one ES index is made up of multiple Lucene indices
- either a single index's multiple shards could be searched, even multiple ES indices could be searched for a term
    - any of this is just combination of multiple Lucene indices
- shard is the main scaling unit in ES

# Components
- Nodes
    - Master
        - Controls the Elasticsearch cluster and is responsible for all cluster-wide operations like creating/deleting an index and adding/removing nodes.
    - Data
        - Stores data and executes data-related operations such as search and aggregation.
    - Client
        - Forwards cluster requests to the master node and data-related requests to data nodes.
- Indices
    - Index
        - Shard
            - Document
- Replicas
    - of shards

Ref:
- https://www.elastic.co/blog/found-elasticsearch-from-the-bottom-up
- https://www.elastic.co/what-is/elasticsearch
- https://www.knowi.com/blog/what-is-elastic-search/
