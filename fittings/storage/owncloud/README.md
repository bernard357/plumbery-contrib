# Personal storage with ownCloud

In this use case we deploy a personal file server based on Owncloud, at the [Managed Cloud Platform from Dimension Data](http://cloud.dimensiondata.com/eu/en/).
This is done with [plumbery](https://docs.mcp-services.net/display/PLUM/Plumbery) and a template that is provided below.

![ownCloud web](owncloud.png)

[ownCloud](https://owncloud.org/) is a self-hosted file sync and share server.
It provides access to your data through a web interface, sync clients or WebDAV while providing a platform to view, sync and share across devices easily — all under your control.
ownCloud’s open architecture is extensible via a simple but powerful API for applications and plugins and it works with any storage.

## Requirements for this use case

* Select a MCP location
* Add a Network Domain
* Add an Ethernet network
* Deploy a Ubuntu server
* Provide 2 CPU and 4 MB of RAM
* Add a virtual disk of 50 GB
* Monitor this server in the real-time dashboard provided by Dimension Data
* Assign a public IPv4 address
* Add address translation to ensure end-to-end IP connectivity
* Add firewall rule to accept TCP traffic on port 22 (ssh) and 80 (web)
* Combine virtual disks into a single expanded logical volume (LVM)
* Update the operating system
* Synchronise node clock
* Install a new SSH key to secure remote communications
* Configure SSH to reject passwords and to prevent access from root account
* Install ownCloud

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

Open a browser window and paste the public address reported by plumbery.
You should receive a welcome HTML page in return. The exciting stuff is to
[synchronize with a tablet or a smartphone](https://owncloud.com/products/mobileapps/) via the same ownCloud instance.

## Destruction commands

Launch following command to remove all resources involved in the fittings plan:

    $ python -m plumbery fittings.yaml dispose

## Use case status

- [ ] Work as expected

## See also

- [Storage services with plumbery](../)
- [All plumbery fittings plans](../../)

