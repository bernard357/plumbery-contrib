# NFS server and client over IPv6 back-end network

The objective of this use case is to deploy a NFS server and a NFS client at two different locations, at the [Managed Cloud Platform from Dimension Data](http://cloud.dimensiondata.com/eu/en/).
This is done with [plumbery](https://docs.mcp-services.net/display/PLUM/Plumbery) and a template that is provided below.

In this tutorial a NFS server is deployed at one data centre, and
a NFS client is deployed at another data centre. The infrastructure and the
nodes are configured to talk to each other over the secured IPv6 back-bone
that ties all MCP together.

## Requirements for this use case

* Select two MCP locations
* Add a Network Domain at each location
* Add an Ethernet network at each location
* Allow IPv6 traffic between the two networks
* Deploy a Ubuntu server at each location
* Monitor these servers in the real-time dashboard provided by Dimension Data
* Add a virtual disk of 100 GB to the server node
* Assign public IPv4 addresses to nodes
* Add address translation to ensure end-to-end IP connectivity
* Add firewall rule to accept TCP traffic on port 22 (ssh)
* Combine virtual disks into a single expanded logical volume (LVM)
* Update the operating system of each node
* Synchronise nodes clock with NTP
* Install a new SSH key to secure remote communications
* Configure SSH to reject passwords and to prevent access from root account
* Add IPv6 addresses to `/etc/hosts` for easy handling
* Install NFS back-end software on server node
* Install NFS client software on client node
* At the client node, change `/etc/fstab` to mount NFS volume automatically
* From the client node, write a `hello.txt` to the server

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

The best is to go to the NFS server via ssh, and to read the file written by
the NFS client in `/var/nfs`.

## Destruction commands

Launch following command to remove all resources involved in the fittings plan:

    $ python -m plumbery fittings.yaml dispose

## Use case status

- [ ] Work as expected

## See also

- [Storage services with plumbery](../)
- [All plumbery fittings plans](../../)

