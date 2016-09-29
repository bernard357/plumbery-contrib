# Plumbery and Apache Libcloud

The objective of this use case is to deploy a plumbery node at the [Managed Cloud Platform from Dimension Data](http://cloud.dimensiondata.com/eu/en/).
This is done with [plumbery](https://developer.dimensiondata.com/display/PLUM/Plumbery) and a template that is provided below.

In many cloud deployments, the appropriate strategy is to run administration
servers directly in the cloud. This usually facilitates a lot end-to-end
connectivity to the other nodes.

For example, Dimension Data provides IPv6 connectivity to every virtual server.
However, very few infrastructure managers do have IPv6 at their workstation.
Therefore the recommendation to deploy a seminal server to the cloud
infrastructure, since this machine will benefit from IPv6 end-to-end.

## Requirements for this use case

* Select a MCP location
* Add a Network Domain
* Add an Ethernet network
* Deploy a Ubuntu node
* Add a virtual disk of 50 GB
* Monitor this server in the real-time dashboard provided by Dimension Data
* Assign a public IPv4 address
* Add address translation to ensure end-to-end IP connectivity
* Add firewall rule to accept TCP traffic on port 22 (ssh)
* Combine the virtual disks into a single expanded logical volume (LVM)
* Update the operating system
* Synchronise node clock with NTP
* Install a new SSH key to secure remote communications
* Configure SSH
* Update `etc/hosts` and `hostnames` to bind IPv6 addresses to host name
* Install python, libcloud and plumbery


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

In this use case you can use the IPv4 assigned to the node for direct ssh
connection.

    $ ssh ubuntu@<ipv4_here>

You will have to accept the new host, and authentication will be based on
the SSH key communicated to the node by Plumbery.

Then you can use this node to deploy any reference fittings plan coming
with `plumbery-contrib`. For example:

    $ cd plumbery-contrib/fittings/messaging/letschat
    $ python -m plumbery fittings.yaml deploy


## Destruction commands

Launch following command to remove all resources involved in the fittings plan:

    $ python -m plumbery fittings.yaml dispose

## Use case status

- [ ] Work as expected

## See also

- [DevOps services with plumbery](../)
- [All plumbery fittings plans](../../)

