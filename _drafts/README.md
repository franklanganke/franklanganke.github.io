Fenced code block:
```
foo
    bar
bazz
```


```
 shipper 1 --|
             |--> broker ---> indexer ---> storage  
 shipper N --|
```


```
IIS/logstash --|
...            |--> AWS SQS --> logstash --> elasticsearch     <-- kibana
IIS/logstash --|
```
