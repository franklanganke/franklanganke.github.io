---
layout: post
title: Centralized logging with logstash on AWS
---

This post gives a short overview of how a centralized logging solution can be designed using [Logstash](http://logstash.net/) on AWS. While skipping the actual configuration (can be looked up) I explain some of the idioms and wording that are frequently used by users and the documentation.

## Analyzing user and application behavior through distributed logs.
Our customers can connect to their Analysis Services Cube's via Excel. The underlying protocol is HTTP so IIS webservers log all access to files. Our ops team needs to monitor the application state:

* What is the current load on all servers? Is the load equally balanced between servers?
* Is the application working (HTTP/200)?
* If not what is the message (without logging into the machine)?

## ELK stack to the rescue: elasticsearch, logstash, kibana
The [ELK](http://www.elasticsearch.org/overview/) stack provides the tools to process (logstash), store (elasticsearch) and visualize (kibana) distributed log files. Older logstash documents and the community use this architectural pattern to describe an event pipeline:

    shipper 1 --|
         ...    |--> broker ---> indexer ---> storage  
    shipper N --|

* shipper  
   Gathers logs on a system and ships them to the broker 
* broker  
    Accepts events from various shippers, can handle lots of in- and outgoing events
* indexer  
   Pulls events from the broker, analyze them and sends them off to different storages
 
Sample setup on AWS:

    IIS/logstash --|
         ...       |--> AWS SQS --> logstash --> elasticsearch <-- kibana
    IIS/logstash --|

## Shipper (or Collector)
The shipper sends the events from the source system to the broker. Note that there is no special mode for logstash to run as a shipper, it is just a pattern. The idea is to have a minimal config, so the event is parsed from a log file and the heavy work is done on a different system. On AWS logstash can send the events to an SQS queue.

* Low system impact (~100MB in memory, low impact on CPU)
* Does few or zero filtering/processing

## Broker
Decouples event source and event processing and can buffer events for the indexer to pick up. SQS is a natural choice within AWS and logstash provides plugins to send to and recieve from an SQS queue.

## Indexer
Again just the ordinary logstash agent, this time configured to do the heavy processing. Pulls events from the broker (SQS), applies filters and sends them to some storage (elasticsearch). 

* High system impact, depending on logstash's worker count CPU utilization can be 100%.
* A couple of T2 Instances are a good choice if the workload is fluctuating.


Mountain pass in California, close to Yosemite NP:
![Tioga Pass](/images/tiogapass.jpg)
