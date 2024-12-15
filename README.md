![Elasticsearch Logo](public/elasticsearch-logo.jpg)

References

- [Docs](https://www.elastic.co/guide/en/elasticsearch/reference/current/elasticsearch-intro-what-is-es.html)
- [Elastic Search Python Package](https://pypi.org/project/elasticsearch/)
- [Python Elastic Search Quickstart](https://elasticsearch-py.readthedocs.io/en/v8.16.0/quickstart.html)
- [Elasticsearch Crash Course](https://youtu.be/a4HBKEda_F8?si=C8jjcKBwS1f-d57y)
- [Elasticsearch Tutorial Github](https://github.com/ImadSaddik/ElasticSearch_Python_Tutorial)

## What is Elasticsearch?

Elasticsearch is a distributed search and analytics engine, scalable data store, and vector database built on Apache Lucene.
It's optimized for speed and relevance on production-scale workloads. Use Elasticsearch to search, index, store, and analyze data of all shapes and sizes in near real time.

## Use Cases

- **Full-text search**: Build a fast, relevant full-text search solution using inverted indexes, tokenization, and text analysis.
- **Vector database**: Store and search vectorized data, and create vector embeddings with built-in and third-party natural language processing (NLP) models.
- **Semantic search**: Understand the intent and contextual meaning behind search queries using tools like synonyms, dense vector embeddings, and learned sparse query-document expansion.
- **Hybrid search**: Combine full-text search with vector search using state-of-the-art ranking algorithms.
- **Build search experiences**: Add hybrid search capabilities to apps or websites, or build enterprise search engines over your organization’s internal data sources.
- **Retrieval augmented generation (RAG)**: Use Elasticsearch as a retrieval engine to supplement generative AI models with more relevant, up-to-date, or proprietary data for a range of use cases.
- **Geospatial search**: Search for locations and calculate spatial relationships using geospatial queries.

## Installation Guide

Install Elastic Search With Docker - [Click Here](https://www.elastic.co/guide/en/elasticsearch/reference/current/docker.html)

1. Create a new docker network

```bash
docker network create elastic
```

2. Pull the Elasticsearch Docker image

```bash
docker pull docker.elastic.co/elasticsearch/elasticsearch:8.17.0
```

3. Start an Elasticsearch container.

```bash
docker run --name es01 --net elastic -p 9200:9200 -it -m 1GB docker.elastic.co/elasticsearch/elasticsearch:8.17.0
```

Machine learning features such as semantic search with ELSER require a larger container with more than 1GB of memory. If you intend to use the machine learning capabilities then start with

```bash
docker run --name es01 --net elastic -p 9200:9200 -it -m 6GB -e "xpack.ml.use_auto_machine_memory_percent=true" docker.elastic.co/elasticsearch/elasticsearch:8.17.0
```

4. Copy the generated elastic password and enrollment token

```bash
docker exec -it es01 /usr/share/elasticsearch/bin/elasticsearch-reset-password -u elastic
docker exec -it es01 /usr/share/elasticsearch/bin/elasticsearch-create-enrollment-token -s kibana
```

5. Copy the SSL Certificate from container to local machine

```bash
docker cp es01:/usr/share/elasticsearch/config/certs/http_ca.crt .
```
