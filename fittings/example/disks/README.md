# Multiple disks added with LVM

The objective of this use case is to deploy a server with extended storage, at the [Managed Cloud Platform from Dimension Data](http://cloud.dimensiondata.com/eu/en/).
This is done with [plumbery](https://docs.mcp-services.net/display/PLUM/Plumbery) and a template that is provided below.

## Requirements for this use case

* Select a MCP location
* Add a Network Domain
* Add an Ethernet network
* Deploy a Ubuntu node
* Add disk 1 with 100 GB of standard storage
* Add disk 2 with 200 GB of standard storage
* Add disk 3 with 30 GB of high-performance storage
* Add disk 4 with 40 GB of high-performance storage
* Add disk 5 with 1000 GB of economy storage
* Add disk 6 with 1000 GB of economy storage
* Monitor this server in the real-time dashboard provided by Dimension Data
* Assign a public IPv4 address
* Add address translation to ensure end-to-end IP connectivity
* Add firewall rule to accept TCP traffic on port 22 (ssh)
* Partition each disk as of Linux LVM type (8e)
* Use LVM to manage logical storage provided by multiple disks
* Extend the mount / with storage brought by disks 1 and 2
* Create new mount /highperformance with combined capacity provided by disks 3 and 4
* Create new mount /economy with combined capacity provided by disks 5 and 6
* Update the operating system
* Synchronise node clock with NTP
* Install a new SSH key to secure remote communications
* Configure SSH to reject passwords and to prevent access from root account

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

    $ sudo fdisk -l
    $ df -h
    $ mount

These commands are self-explanatory and validate disks deployment and configuration.

## Destruction commands

Launch following command to remove all resources involved in the fittings plan:

    $ python -m plumbery fittings.yaml dispose

## Use case status

- [ ] Work as expected

## See also

- [Example configurations with plumbery](../)
- [All plumbery fittings plans](../../)

