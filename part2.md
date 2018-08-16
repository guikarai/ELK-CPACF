# Step 2 - Starting an ELK on LinuxONE for Monitoring Cryptographic Activities

In this part, you will learn how to monitor captured LinuxONE crypto activity thanks to APIs. You will send these captured information to a no-slq database (Elasticsearch Database).

## What the ELK..?!
Elasticsearch is a search engine based on Lucene. It provides a distributed, multitenant-capable full-text search engine with an HTTP web interface and schema-free JSON documents. Elasticsearch is developed in Java and is released as open source under the terms of the Apache License. Official clients are available in Java, .NET (C#), PHP, Python, Apache Groovy, Ruby and many other languages. According to the DB-Engines ranking, Elasticsearch is the most popular enterprise search engine followed by Apache Solr, also based on Lucene.

Elasticsearch is developed alongside a data-collection and log-parsing engine called Logstash, and an analytics and visualisation platform called Kibana. The three products are designed for use as an integrated solution, referred to as the "Elastic Stack" (formerly the "ELK stack").

Elasticsearch can be used to search all kinds of documents. It provides scalable search, has near real-time search, and supports multitenancy. "Elasticsearch is distributed, which means that indices can be divided into shards and each shard can have zero or more replicas. Each node hosts one or more shards, and acts as a coordinator to delegate operations to the correct shard(s). Rebalancing and routing are done automatically". Related data is often stored in the same index, which consists of one or more primary shards, and zero or more replica shards. Once an index has been created, the number of primary shards cannot be changed.

More information about ELK here: https://www.elastic.co

## What to keep in mind about ELK?
"ELK" is the acronym for three open source projects: Elasticsearch, Logstash, and Kibana. 

* Elasticsearch is a search and analytics engine. 
* Logstash is a server‑side data processing pipeline that ingests data from multiple sources simultaneously, transforms it, and then sends it to a "stash" like Elasticsearch. 
* Kibana lets users visualize data with charts and graphs in Elasticsearch. 

The Elastic Stack is the next evolution of ELK.



## Cloning the ELK-CPACF github repository

First of all, let's install the lab required components and their dependencies in your LinuxONE Linux guest. Please issue the following command:
```
yum install docker-ce docker-compose git curl
```

Once done, it now time to clone the github repository of this code pattern. Please issue the following command:
```
git clone https://github.com/guikarai/ELK-CPACF.git
```

Now, let's explore the content of the ELK-CPACF git. Please issue the following command:
```
ls -l

  total 72
  drwxr-xr-x 3 root root  4096 Aug 16 15:00 ELK
  -rw-r--r-- 1 root root  3504 Aug 16 15:06 README.md
  -rw-r--r-- 1 root root    26 Aug 16 15:06 _config.yml
  drwxr-xr-x 3 root root  4096 Aug 16 15:12 icastats
  drwxr-xr-x 2 root root  4096 Aug 16 15:06 images
  -rw-r--r-- 1 root root 29456 Aug 16 15:06 part1.md
  -rw-r--r-- 1 root root  7768 Aug 16 15:06 part2.md
  -rw-r--r-- 1 root root  6759 Aug 16 15:06 part3.md
  -rw-r--r-- 1 root root  2785 Aug 16 15:10 vmstat-script.sh
```

**Important content regarding the code pattern:**
* ELK/      : Directory about the ELK docker stack and configuration.
* vmstat-script    : Main script to start to collect local vmstats and to push to Elasticsearh.
* icastats/  : Directory containing main scripts to start to collect local icastats and to push to Elasticsearh.

**Github administrative content:**
* images/     : Administrative folder to store illustrations.
* README.md   : Administrative git landing page.
* _config.yml : Administrative git landing page.
* part1.md    : Administrative git landing page of part1.
* part2.md    : Administrative git landing page of part2.
* part3.md    : Administrative git landing page of part3.


## Deploying an ELK Docker stack

Let's move inside the ELK/ repository. Please issue the following command:
```
cd  ELK/
```

Let's brows the content of this directory. Please issue the following command:
```
ls -l

  total 8
  drwxr-xr-x 2 root root 4096 Aug 16 14:26 config
  -rw-r--r-- 1 root root  847 Aug 16 14:46 docker-compose.yml
```

**Note:**

* config/             :   This is a directory containing configuration file of Logstash, Kibana and Elasticsearch.
* docker-compose.yml  :   This is a docker-compose file describing how to start and with which configuration containers of Logstash, Kibana and Elasticsearch from images.

We are now ready to deploy the ELK docker based stack. Please issue the following command:
```
docker ps
CONTAINER ID        IMAGE                                      COMMAND               CREATED             STATUS              PORTS                                                                                                    NAMES
```

As you can see, there is no running containers. This is normal. Now let's pull the docker base ELK stack using the docker-compose file. Please issue the following command:
```
docker-compose -f docker-compose.yml up -d

  Creating Elasticsearch
  Creating Kibana
  Creating Logstash
```

Let's check that the ELK stack run properly. Please issue the following command:
```
docker ps

  CONTAINER ID        IMAGE                                      COMMAND               CREATED             STATUS              PORTS                                                                                                    NAMES
  94c1e73369ff        hyperledgerlinuxone/kibana:latest          "kibana -H 0.0.0.0"   3 seconds ago       Up 2 seconds        0.0.0.0:514->514/tcp, 0.0.0.0:5000->5000/tcp, 0.0.0.0:5043->5043/tcp, 0.0.0.0:9292->9292/tcp, 5601/tcp   Logstash
  fdafc035465d        hyperledgerlinuxone/kibana:latest          "kibana -H 0.0.0.0"   12 minutes ago      Up 12 minutes       0.0.0.0:5601->5601/tcp                                                                                   Kibana
  fdbef59b18b3        hyperledgerlinuxone/elasticsearch:latest   "elasticsearch"       12 minutes ago      Up 12 minutes       0.0.0.0:9200->9200/tcp, 0.0.0.0:9300->9300/tcp                                                           Elasticsearch

```

As you can see, there are 3 running docker containers: Elasticsearch, Kibana and Logstash.

Please check that the following URL return something to you:
* YourIP-Address:9200  : Elasticsearch technical message indicating everything is alright
* YourIP-Address:5601  : Main Kibana landing page

## Tooling for Elasticsearch
To see with a user friendly interface the status of your elasticsearch instance, please, install in your computer the elasticsearch web-plugin named elasticsearch-head. 

Fill in the form and connect to your elasticsearch instance with the appropriate IP adress. The portname is by default 9200.
Eg. http://<@IP>:9200. 
  
You should be able to see something simillar to the following:
![alt text](https://github.com/guikarai/ELK-CPACF/blob/master/images/Capture%20d%E2%80%99e%CC%81cran%202018-06-20%20a%CC%80%20170639%20(2).png)

## Seting-up local linux and crypto data collection
### Linux VMSTATS Data collection
First of all, let's move backward in the cloned git repository. Please issue the following command:
```
cd ..
```

Now, let's configure the first data source made of Linux vmstats. To collect and to push these data to elasticsearch db we will use a script. Let's start to modify this script to adhere with your environment. Please, correct the default ESserverIP adress with your @IP adress according to your environment. Change the 2 line as show below:
```
vi vmstat-script.sh
  #!/bin/bash
  ESserverIP="127.0.0.1" <--- Change with your IP address here
```

Now, let's make this script executable thanks to following command:
```
chmod +x vmstat-script.sh
```

Let's start now the VMSTAT data collection. Please use the following command:
```
./vmstat-script.sh&
```
It is normal to see every 5 seconds a new line being displayed.

You can verify that there are new documents pushed to elasticsearch db thanks to your web browser tool. If you check it, and if you set the refresh to "Refresh every 5s" in the top-right corner, you should be able to see something as the following:

![alt-text](https://github.com/guikarai/ELK-CPACF/blob/master/images/elasticsearch-tool-vmstat.png)


Please, now open a new ssh session to your LinuxONE Linux guest.

### Linux crypto ICASTATS Data collection

In your new LinuxONE Linux guest, please move to the the cloned git repository. Please issue the following command:
```
cd ELK-CPACF/
```

Now, let's configure the main data source made of Linux crypto ICASTATS. To collect and to push these data to elasticsearch db we will use a script. Let's start to modify this script to adhere with your environment. Please, correct the default ESserverIP adress with your @IP adress according to your environment. Change the 2 line as show below:
```
vi icastats/crypto-monitoring.sh
  #!/bin/bash
  ESserverIP="127.0.0.1" <--- Change with your IP address here
```

Now, let's make this script executable thanks to following command:
```
chmod +x icastats/crypto-monitoring.sh
```

Let's start now the VMSTAT data collection. Please use the following command:
```
./icastats/crypto-monitoring.sh&

  {"_index":"monitor-icastats","_type":"icastats","_id":"Rnn7QmUBe_nBz08EzK4S","_version":1,"result":"created","_shards":{"total":2,"successful":1,"failed":0},"_seq_no":0,"_primary_term":1}sendToES 1534427122 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 169
  {"_index":"monitor-icastats","_type":"icastats","_id":"R3n7QmUBe_nBz08E367i","_version":1,"result":"created","_shards":{"total":2,"successful":1,"failed":0},"_seq_no":0,"_primary_term":1}sendToES 1534427127 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
  ...
```

It is normal to see every 5 seconds a new line being displayed. Ervery 5 seconds, a record will be sent to the elasticsearch db. 

To assess that it works properly, with web interface there are new records added in the elasticsearch db.
Your elasticsearh web interface should look like the foolowing:

![alt text](https://github.com/guikarai/ELK-CPACF/blob/master/images/elasticsearch-tool-vmstat-icastats.png)

You are now good for the part 3 about creating a dashboard to magnify live captured crypto information.
