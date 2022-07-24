# Apache Pulsar

## Overview
- multi-tenant
- scalability
- persistent messages
- sequenced, guaranteed messaging
- work queue
- once messaging

## Concepts
- Tenant
  - Topics
- Broker, Bookkeeper, Zookeeper
  - Broker - message routing, connections, stateless (with caches), auto load balancing, topics (multiple segments)
  - Bookkeeper - bookies, store messages, grouped in segments/ledgers, group of bookies (ensemble) to store a ledger
  - Zookeeper - metadata store, service discovery, instead may use RocksDB/etcd
- Sequenced event stream
- Reader, Batch API
- Pub/Sub messaging queue
- Message (Value/data payload, Key, Properties, ProducerName, SequenceID)
- 


```
bin/pulsar standalone
bin/pulsar sql-worker start
bin/pulsar-admin
tenants create conference
namespaces create conference/pythonweb
tenants list
namespaces list conference
topics create persistent://conference/pythonweb/first
topics list conference/pythonweb

python3 -m pip install pulsar-client=='2.9.1[all]'

import pulsar

client = pulsar.Client('pulsar://localhost:6650')
producer = client.create_producer('persistent://conference/pythonweb/first')
producer.send('Simple text message').encode('utf-8')
client.close()
```

pulsar manager

```
import time, weatherhat
import pulsar
import logging, sys, datetime, subprocess, os, traceback math, base64, json, psutil, uuid
from time import gmtime, strftime, sleep
import random, string
from math import isnan
from subprocess import PIPE, Popen
import socket
from pulsar.schema import *

class weather(Record):
    uuid = String()
    ipaddress = String()
    cputempf = Integer()
    runtime = Integer()
    host = String()
    hostname = String()
    macaddress = String()
    endtime = String()


def IP_address():
    ...

```

https://github.com/tspannhw/pulsar-pychat-function/blob/main/src/sentiment.py
https://github.com/streamnative/examples/blob/master/cloud/python/OAuth2Producer.py
