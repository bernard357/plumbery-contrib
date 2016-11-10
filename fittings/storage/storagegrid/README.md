# StorageGRID Webscale cluster of 4 nodes

The objective of this use case is to deploy a cluster of StorageGRID nodes at the [Managed Cloud Platform from Dimension Data](http://cloud.dimensiondata.com/eu/en/).
This is done with [plumbery](https://docs.mcp-services.net/display/PLUM/Plumbery) and a template that is provided below.

![Architecture](architecture.png)

The cluster is built out of 4 nodes, plus an additional gateway, that is acting as a load balancer across the storage nodes.
There is also an administration node that is used to manage access to the objects.

This is effectively creating an Object-Based Storage (OBS) back-end, that is fully compatible with the protocol of AWS for their S3 service.
In other terms, we re-create here a private S3-like facility on the MCP itself.

## Requirements for this use case

* Select a MCP location where custom NetApp images have been put in client library
* Add a Network Domain
* Add an Ethernet network
* Deploy nodes using the custom virtual appliances from the client library
* Monitor all nodes in the real-time dashboard provided by Dimension Data
* Assign a public IPv4 address to each node
* Add address translation rules to ensure Internet connectivity with each server
* Add firewall rule to accept TCP traffic on specific ports for each node

## Fittings plan

[Click here to read fittings.yaml](fittings.yaml)

## Deployment command

    $ python -m plumbery fittings.yaml deploy

This command will build fittings as per the provided plan and start each node.
Look at messages displayed by plumbery while it is
working, so you can monitor what's happening.

## Follow-up commands

Since most nodes are coming out of Validated Workload process,
there is a need to use specific instructions from ITaaS when new node is deployed.
Unfortunately this cannot be orchestrated and has to be done manually.

## Destruction commands

Launch following command to remove all resources involved in the fittings plan:

    $ python -m plumbery fittings.yaml dispose

## Use case status

- [X] Work as expected

## See also

- [Storage with plumbery](../)
- [All plumbery fittings plan](../../)

