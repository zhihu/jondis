# Jondis

Jondis is a high availability pool management class for the excellent https://github.com/andymccurdy/redis-py

[![Build Status](https://travis-ci.org/youngking/jondis.svg)](https://travis-ci.org/youngking/jondis)


## Features

* Slave discovery on startup
* On master failure, if a slave is promoted, the pool will reconfigure to connect to the new master


## Limitations

* Currently all commands are sent to the master
* No master discovery if only a slave server is provided
* In certain scenarios, the pool will pick up new slaves (if it's reconfigured), but
  there's currently no periodic / automatic slave discovery
* Does not talk to sentinel


## Requirements

redis-py


## Usage

In order to configure the pool, you'll need to provide at least 1 active master server.  This is a limitation that
will be lifted soon with master discovery.

```python
from jondis.pool import Pool
from redis import Redis
pool = Pool(hosts=["redis01:6379", "redis02:6379"])
redis = Redis(connection_pool=pool)
```

or

```python
from jondis.client import create_client
hosts = ["redis01:6379", "redis02:6379"]
redis = create_client(hosts)
```
