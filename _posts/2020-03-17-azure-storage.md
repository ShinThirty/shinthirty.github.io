---
layout: post
title:  "Azure Storage"
date:   2020-03-17
categories: [note]
tags:   [system design]
---

## Tenets

1. RPC vs REST api

2. Use DNS to analyze the account name in the input URI and route the request to the correct storage stamp

3. Use location service to update DNS record on which storage stamp the data of the new users should be stored

4. Maintain the utilization of each storage stamp to 70% to 80%

5. Storage stamp consists of front end layer, partition layer and stream layer

6. Front end layer is responsible for pre-processing and authentication of the request

7. Partition layer and stream layer has a N-to-N mapping relationship

8. Partition layer is a highly available key-value storage a.k.a object table (OT)

9. Each stream layer service is similar to the NameNode in HDFS

10. Locking service provides a distributed locking mechanisum to prevent incoming requests when the mapping to partition layer (partition service)

11. Stream layer is composed of stream manager (SM) and extent node (EN)

12. Use Erasure Coding to save storage space

## Reference

[Windows Azure Storage](https://www.sigops.org/s/conferences/sosp/2011/current/2011-Cascais/printable/11-calder.pdf)
