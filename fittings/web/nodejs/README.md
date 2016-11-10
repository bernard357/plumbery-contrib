# Linux-Nginx-MySQL-PHP web server (LEMP)

The objective of this use case is to deploy a web server powered by Node.js, at the [Managed Cloud Platform from Dimension Data](http://cloud.dimensiondata.com/eu/en/).
This is done with [plumbery](https://docs.mcp-services.net/display/PLUM/Plumbery) and a template that is provided below.

Are you more familiar with javascript? Ok, let's continue with a
different flavour of web site, powered by Node.js.

## Requirements for this use case

* Select a MCP location
* Add a Network Domain
* Add an Ethernet network
* Deploy a Ubuntu server
* Provide 2 CPU and 8 MB of RAM
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
* Remove Apache
* Install Node.js and PM2
* Provide a sample "hello world" application written in javascript

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
You will receive a welcome HTML page in return.

## Destruction commands

Launch following command to remove all resources involved in the fittings plan:

    $ python -m plumbery fittings.yaml dispose

## Use case status

- [ ] Work as expected

## See also

- [Web services with plumbery](../)
- [All plumbery fittings plans](../../)

