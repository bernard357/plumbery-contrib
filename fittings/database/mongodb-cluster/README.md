# Cluster of MongoDB servers

The objective of this use case is to pool multiple MongoDB servers, at the [Managed Cloud Platform from Dimension Data](http://cloud.dimensiondata.com/eu/en/).
This is done with [plumbery](https://docs.mcp-services.net/display/PLUM/Plumbery) and a template that is provided below.

MongoDB is a database that is really well-adapted to NoSQL storage and to real-time data analytics.
In this use case we will deploy multiple servers, and glue them together.

## Requirements for this use case

* Select a MCP location
* Add a Network Domain
* Add an Ethernet network
* Deploy multiple Ubuntu servers
* Add a virtual disk to selected nodes
* Monitor these servers in the real-time dashboard provided by Dimension Data
* Assign public IPv4 addresses to nodes
* Add address translation to ensure end-to-end IP connectivity
* Add firewall rule to accept TCP traffic on port 22 (ssh)
* Combine virtual disks into a single expanded logical volume (LVM)
* Update the operating system of each node
* Synchronise nodes clock with NTP
* Install a new SSH key to secure remote communications
* Configure SSH to reject passwords and to prevent access from root account
* Add MongoDB to all servers
* Create a cluster of configuration servers
* Add sharding servers

## Fittings plan

[Click here to read fittings.yaml](fittings.yaml)

## Deployment command

    $ python -m plumbery fittings.yaml deploy

This command will build fittings as per the provided plan, start the server
and bootstrap it. Look at messages displayed by plumbery while it is
working, so you can monitor what's happening.

## Follow-up commands

At the end of the deployment, plumbery will display on screen some instructions
to help you move forward. You can ask plumbery to display this information
at any time with the following command:

    $ python -m plumbery fittings.yaml information

TO BE COMPLETED

## Destruction commands

Launch following command to remove all resources involved in the fittings plan:

    $ python -m plumbery fittings.yaml dispose

## Use case status

- [ ] Work as expected

## See also

- [Database services with plumbery](../)
- [All plumbery fittings plans](../../)

