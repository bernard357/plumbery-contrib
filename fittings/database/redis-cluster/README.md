# Cluster of Redis servers

The objective here is to deploy a cluster of redundant Redis servers, at the [Managed Cloud Platform from Dimension Data](http://cloud.dimensiondata.com/eu/en/).
This is done with [plumbery](https://docs.mcp-services.net/display/PLUM/Plumbery) and a template that is provided below.

[Redis](http://redis.io/) is an open source (BSD licensed), in-memory data structure store, used as database, cache and message broker.
It supports data structures such as strings, hashes, lists, sets, sorted sets with range queries, bitmaps, hyperloglogs and geospatial indexes with radius queries.
Redis is providing superior performance to web sites and to application servers.
In this use case we orchestrate a master Redis node and 3 slave redis nodes.

## Requirements for this use case

* Select a MCP location
* Add a Network Domain
* Add an Ethernet network
* Deploy 4 Ubuntu nodes
* Provide 2 CPU and 4 MB of RAM
* Monitor this server in the real-time dashboard provided by Dimension Data
* Assign a public IPv4 address
* Add address translation to ensure end-to-end IP connectivity
* Add firewall rule to accept TCP traffic on port 22 (ssh)
* Update the operating system
* Synchronise node clock
* Install a new SSH key to secure remote communications
* Configure SSH to reject passwords and to prevent access from root account
* Add Redis to all nodes
* Configure one server as the master
* Configure other servers to replicate the master

## Fittings plan

[Click here to read fittings.yaml](fittings.yaml)

## Deployment command

    $ python -m plumbery fittings.yaml deploy

This command will build fittings as per the provided plan, start the server
and bootstrap it. Look at messages displayed by plumbery while it is
working, so you can monitor what's happening.

## Follow-up commands

At the end of the deployment, plumbery will display the secret used to
authenticate to the redis master server. You can ask plumbery to display this information
at any time with the following command:

    $ python -m plumbery fittings.yaml information

After the setup, connect via ssh to redis01 to check the status of the cluster::

    $ ssh ubuntu@<ipv4_of_redis01>
    $ redis-cli -h 127.0.0.1 -p 6379
    > AUTH {{ random.secret }}
    OK
    > INFO
    ...
    # Replication
    role:master
    connected_slaves:3

## Destruction commands

Launch following command to remove all resources involved in the fittings plan:

    $ python -m plumbery fittings.yaml dispose

## Use case status

- [ ] Work as expected

## See also

- [Database services with plumbery](../)
- [All plumbery fittings plans](../../)

