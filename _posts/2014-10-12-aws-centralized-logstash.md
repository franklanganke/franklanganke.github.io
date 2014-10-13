---
layout: post
title: Centralized logging with logstash on AWS
---

*this is a draft*

## Analyzing user and application behavior through distributed logs.
Our customers can connect to their Analysis Services Cube's via Excel and ops team needs to monitor the application state:

* What is the current load on all servers? Is the load equally balanced between servers?
* Is the application working (HTTP/200)?
* If not what is the message (without logging into the machine)?

So the task is to analyze IIS log files and make results viewable for different groups.

## ELK stack: elasticsearch, logstash, kibana
The ELK stack provides the tools to process (logstash), store (elasticsearch) and visualize (kibana) distributed log files. Older logstash documents and the community use this architectural pattern to describe an event pipeline:


    shipper 1 --|
                |--> broker ---> indexer ---> storage  
    shipper N --|


* shipper

 Gathers logs on a system and ships them to the broker 
* broker

 Accepts events from various shippers, can handle lots of in- and outgoing events
* indexer

 Pulls events from the broker, analyze them and sends them off to different storages
 
Sample setup on AWS:

```
IIS/logstash --|
...            |--> AWS SQS --> logstash --> elasticsearch     <-- kibana
IIS/logstash --|
```


## AWS pipeline

## Housekeeping
* deleting indexes
* restarting logstash


Mountain pass in California, close to Yosemite NP:
![Tioga Pass](/images/tiogapass.jpg)
