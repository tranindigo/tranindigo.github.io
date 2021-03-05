---
title: "AWS Elasticache Caching Strategies"
date: "2020-07-19"
categories: 
  - "aws"
tags: 
  - "elasticache"
  - "lazy-loading"
  - "memcached"
  - "redis"
  - "write-through"
---

Caching strategies dictate how you can populate and access data in the cache. There are two main strategies that AWS Elasticache uses: lazy loading and write-through.

## Lazy Loading

Lazy loading, also known as cache-aside caching, is a popular caching strategy. It works like the following:

1. When your application needs to read data from a database, it checks the cache first to determine whether the data is available.
2. If the data is available (a cache hit), the cached data is returned.
3. If the data is not available (a cache miss), your application queries the database for the data. Your application then updates the cache with the data that is retrieved from the database. The data is then returned.

## Write-Through

A write-through cache strategy basically updates the cache with every database call. It can be summarized like the following:

1. Your application updates the primary database.
2. Immediately afterward, the data is also updated in the cache.

## So which caching strategy is better?

It depends! The write-through strategy ensures that the cache is up-to-date with the database, so there is a better chance that the data will be found in the cache. This will result in better overall application performance because there are fewer database reads and more cache reads. On the other hand, the write-through approach ensures that all data is written to the cache, which means that infrequently-accessed data is also written, which results in a more expensive cache.

## Redis versus Memcached

AWS offers two types of managed caching solutions: Redis and Memcached. Both tools are powerful, fast, in-memory data stores. However, there are important differences that you need to be aware of when choosing between these two.

First, Memcached is a simple volatile cache server that stores basic key/value pairs where the value has a cap of 1MB. Redis, on the other hand, can store values up to 512MB. However, an important difference is that the data in Redis will persist even when the cache service is restarted. In Memcached the data will not restart.

Secondly, Memcached can only store String values while Redis is a data structure server that can serve many different data types, such as Strings, Hashes, Lists, Sets, Sorted Sets, and Geo (geographic data).

Finally, Memcached is multi-threaded and fast while Redis has lots of features but is completely limited to one core since it is based on an event loop.

## Summary

So when you need to understand how caches work and the different caching strategies, know that both lazy loading and write-through are used with almost all modern caches. Furthermore, AWS offers a managed cache service, Elasticache, through either Memcached or Redis. The decision to choose either Memcached or Redis can be reduced to key characteristics between the two cache systems. Only you know your application's use case. Choose wisely!
