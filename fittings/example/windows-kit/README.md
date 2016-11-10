# A kit of multiple nodes using Microsoft Windows operating system

The objective of this use case is to deploy consistent kits of Microsoft Windows nodes, at the [Managed Cloud Platform from Dimension Data](http://cloud.dimensiondata.com/eu/en/).
This is done with [plumbery](https://docs.mcp-services.net/display/PLUM/Plumbery) and a template that is provided below.

## Requirements for this use case

* Select a MCP location
* Add a Network Domain
* Add one Ethernet network to map external access to selected nodes (via RDS)
* Add one Ethernet network per kit of Windows nodes
* Deploy multiple nodes per kit: DC, IIS, Exchange, ...
* Monitor each server in the real-time dashboard provided by Dimension Data
* Set all private IPv4 addresses statically

## Fittings plan

[Click here to read fittings.yaml](fittings.yaml)

## Deployment command

    $ python -m plumbery fittings.yaml deploy

This command will build fittings as per the provided plan, start the server
and bootstrap it. Look at messages displayed by plumbery while it is
working, so you can monitor what's happening.

## Follow-up commands

At the end of the deployment, plumbery will list available nodes. You can ask plumbery to display this information
at any time with the following command:

    $ python -m plumbery fittings.yaml information

You can connect privately to each node with RDP using the private on-demand VPN coming with the Managed Cloud Platform.
This is based on Cisco AnyConnect technology.

## Destruction commands

Launch following command to remove all resources involved in the fittings plan:

    $ python -m plumbery fittings.yaml dispose

## Use case status

- [ ] Work as expected

## See also

- [Example configurations with plumbery](../)
- [All plumbery fittings plans](../../)

