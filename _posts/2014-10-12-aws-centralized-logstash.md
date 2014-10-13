---
layout: post
title: Centralized logging with logstash on AWS
---

*this is a draft*

## Analyzing user and application behavior through distributed logs.
Our customers can connect to their Analysis Services Cube's via Excel. While our product team tracks user actions our ops team needs to monitor the application state:
* What is the current load on all servers? Is the load equally balanced between servers?
* Is the application working (HTTP/200)?
* If not what is the message (without logging into the machine)?

So the task is to analyze IIS log files and make results viewable for different groups.

## Enter logstash
*logstash, elasticsearch, kibana
*shipper
*broker
*indexer

## AWS pipeline

## Housekeeping
* deleting indexes
* restarting logstash


Mountain pass in California, close to Yosemite NP:
![Tioga Pass](/images/tiogapass.jpg)
