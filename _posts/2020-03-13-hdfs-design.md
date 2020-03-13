---
layout: post
title:  "HDFS Design Concepts"
date:   2020-03-13
categories: [note]
tags:   [system design]
---

## Tenets

1. HDFS basic architecture: [Official Document](https://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsDesign.html)

2. Read and write operation work flow

3. Security and authorization: [Public-key cryptography](https://en.wikipedia.org/wiki/Public-key_cryptography)

4. High availibility design, how to duplicate NameNode and synchronize between them, journaling

5. Failove and recover

6. HDD vs SSD vs ram disk

7. How to add new DataNode and how to balance between old, occupied DataNode and new, empty ones

8. Federation, sync between different HDFS cluster to allow even bigger scale, client-based federation and router-based federation
