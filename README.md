# Cassandra + Spark Cluster

This repository provides everything you need to run Cassandra Cluster in Docker, and is tuned for fast container startup.

## Getting started
```
$ git clone https://github.com/eSolutionsGrup/cassandra-spark-cluster.git
$ cd cassandra-spark-cluster
$ docker-compose up -d
```

Run _docker-compose ps_ to list your Cassandra nodes:
```
$ docker-compose ps
             Name                           Command               State                                                              Ports                                                            
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
cassandrasparkcluster_node01_1   /docker-entrypoint.sh cass ...   Up      0.0.0.0:7000->7000/tcp, 0.0.0.0:7001->7001/tcp, 0.0.0.0:7199->7199/tcp, 0.0.0.0:9042->9042/tcp, 0.0.0.0:9160->9160/tcp      
cassandrasparkcluster_node02_1   /docker-entrypoint.sh cass ...   Up      0.0.0.0:17000->7000/tcp, 0.0.0.0:17001->7001/tcp, 0.0.0.0:17199->7199/tcp, 0.0.0.0:19042->9042/tcp, 0.0.0.0:19160->9160/tcp 
cassandrasparkcluster_node03_1   /docker-entrypoint.sh cass ...   Up      0.0.0.0:27000->7000/tcp, 0.0.0.0:27001->7001/tcp, 0.0.0.0:27199->7199/tcp, 0.0.0.0:29042->9042/tcp, 0.0.0.0:29160->9160/tcp 

```

After starting check cluster status, run this in the container (```docker exec -ti `docker ps --format '{{.Names}}' | grep node01` bash```)
```
nodetool status
```
If the cluster started correctly you should see back a few lines, three of them starting with UN, like this
```
Datacenter: datacenter1
=======================
Status=Up/Down
|/ State=Normal/Leaving/Joining/Moving
--  Address      Load       Tokens       Owns    Host ID                               Rack
UN  192.168.0.2  4.9 MiB    256          ?       516367f2-684b-48c0-8edf-cb653a44ef5b  rack1
UN  192.168.0.3  3.14 MiB   256          ?       0aeccf1a-d86f-4bec-968c-cfdea9fb019b  rack1
UN  192.168.0.4  3.5 MiB    256          ?       9fa89b89-ae38-49c6-8c1a-f8c7c1d50359  rack1
```
This means that all the nodes are up (U) and operating normally (N)
