---
layout: default
title: elasticsearch
---
#Elasticsearch study note
Recently i have encountered with **[Elasticsearch](https://www.elastic.co/)**,my work ask me to study elasticsearch.
So here are my study note.

This [site](http://www.hubwiz.com/course/55473b0aebfde9b5591bb80a/) is very good to study elasticsearch.It can help you get much more than read some big and heavy books.

Here are many [plugin](http://www.cnblogs.com/huangfox/p/3541300.html) you can use,what plugin i am using is **elasticsearch-head** you can visit in your browser by type :127.0.0.1:9200/_plugin/head

type command:
```
curl -XGET 'http://localhost:9200/_count?pretty'
```
return:

    {
    "count" : 12584995,
    "_shards" : {
    "total" : 5,
    "successful" : 5,
    "failed" : 0
    }
    }
this [blog](http://blog.csdn.net/july_2/article/details/24730151) is nice  to study es.

This [site](http://www.sxt.cn/u/2540/blog/3592) tell you how to find the ikanalyzer's core source code.

the[ElasticSearch Java api](http://www.bubuko.com/infodetail-648214.html) tell you which query type you should choose,and you can see [this](http://www.cnblogs.com/yjf512/p/4897294.html) too.

[ElasticSearch Users](http://elasticsearch-users.115913.n3.nabble.com/)