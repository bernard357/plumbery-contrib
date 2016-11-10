# The master plan to conquer the world

In this use case we demonstrate how a large number of nodes can be deployed at the [Managed Cloud Platform from Dimension Data](http://cloud.dimensiondata.com/eu/en/).
This is done with [plumbery](https://docs.mcp-services.net/display/PLUM/Plumbery) and a template that is provided below.

The goal of GigaFox is to deploy a global infrastructure involving
multiple resources spread in different regions and connected to each other.
Their fittings plan is the biggest of all.

Multiple blueprints are provided in this use case, and each of them can be handled separately.
Also, since plumbery is working in parallel as much as possible, the full deployment of all nodes can take place
in a reasonable amount of time.

## Requirements for this use case

* Select multiple MCP locations
* Create Network Domains at each location
* Create Ethernet networks at each location
* Deploy various workloads

## Fittings plan

[Click here to read fittings.yaml](fittings.yaml)

## Deployment command

For this use case plumbery has to connect separately to multiple data centres
and to apply several changes in multiple waves.

    $ python -m plumbery fittings.yaml deploy

This command will build fittings as per the provided plan, and start
servers as well. Look at messages displayed by plumbery while it is
working, so you can monitor what's happening.

## Destruction commands

Cloud computing has a hard rule. Any resource has a cost, be it used or not.
At the end of every session, you are encouraged to destroy everything.
Hopefully, plumbery is making this really simple:

    $ python -m plumbery fittings.yaml dispose

## Use case status

- [ ] Work as expected

## See also

- [Example configurations with plumbery](../)
- [All plumbery fittings plan](../../)

