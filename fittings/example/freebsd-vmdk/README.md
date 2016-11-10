# FreeBSD node installed from custom VMDK (experimental)

This is a minimal project, where one FreeBSD node is deployed at the [Managed Cloud Platform from Dimension Data](http://cloud.dimensiondata.com/eu/en/).
This is done with [plumbery](https://docs.mcp-services.net/display/PLUM/Plumbery) and a template that is provided below.

Warning: this use case is provided only for experimentations. At this point in
time FreeBSD is not supported by Dimension Data.

![FreeBSD](freebsd.png)

The idea is to deploy a small Ubuntu node first, and then to write a VMDK on
a large virtual disk. Then the boot sequence is modified to boot the
FreeBSD kernel directly.

## Requirements for this use case

* Select a MCP location
* Add a Network Domain
* Add an Ethernet network
* Deploy a Ubuntu node
* Add a disk for FreeBSD
* Monitor this server in the real-time dashboard provided by Dimension Data
* Assign a public IPv4 address
* Add address translation to ensure end-to-end IP connectivity
* Add firewall rule to accept TCP traffic on port 22 (ssh)
* Download the VMDK of a FreeBSD virtual server
* Convert the VMDK to /dev/sdb
* Change the boot sequence with GRUB
* Reboot the node on FreeBSD

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

Since no network information is given to the FreeBSD node, it cannot be
accessed over the Internet. The only way to login to the machine is to use the
console access, via the Cloud Control web user interface.

The VMDK is downloaded from osboxes.org, and you can get credentials
by browsing [the FreeBSD page at osboxes](http://www.osboxes.org/freebsd/).

The name and password can be put in the console access to the node, as expected.

![menu](menu.png)

## Troubleshooting

This use case is purely experimental, and has the only merit to demonstrate
how different building blocks can be orchestrated to run a custom VMDK on the MCP.

It takes significant time to deploy because of heavy operations:

* Deployment of a ubuntu node
* Download of the VMDK from a public web site
* Conversion of the VMDK to /dev/sdb

So once plumbery has finished its job, cloud-init may need 10 to 12 minutes
to complete the full deployment and reboot to FreeBSD. In the meantime, you
may want to connect to the node while it is still running ubuntu, and check
progress of cloud-init:

    $ ssh ubuntu@<ipv4_here>
    $ cat /var/log/cloud-init-output.log

## Destruction commands

Launch following command to remove all resources involved in the fittings plan:

    $ python -m plumbery fittings.yaml dispose

## Use case status

- [X] Work as expected

## See also

- [Example configurations with plumbery](../)
- [All plumbery fittings plans](../../)

