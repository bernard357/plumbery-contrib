# Cluster of Apache web servers behind the load-balancer integrated in the Managed Cloud Platform

The objective of this use case is to pool multiple web server, at the [Managed Cloud Platform from Dimension Data](http://cloud.dimensiondata.com/eu/en/).
This is done with [plumbery](https://docs.mcp-services.net/display/PLUM/Plumbery) and a template that is provided below.

The web service is accessible from the Internet via a single public IPv4 address. Traffic is balanced across available
web servers by the load-balancer that is coming with the Managed Cloud Platform itself.

## Requirements for this use case

* Select a MCP location
* Add a Network Domain
* Add an Ethernet network
* Deploy 10 web servers
* Monitor these servers in the real-time dashboard provided by Dimension Data
* Pool servers
* Add a listener and configure load-balancing
* Assign a public IPv4 address to the load-balancer
* Add address translation to ensure end-to-end IP connectivity
* Add firewall rule to accept TCP traffic on port 22 (ssh) and 80 (web)
* Update the operating system
* Synchronise node clock with NTP
* Install a new SSH key to secure remote communications
* Configure SSH to reject passwords and to prevent access from root account
* Install Apache2 and PHP
* Reflect server name at web home pages

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
You should receive a welcome HTML page in return.

## Destruction commands

Launch following command to remove all resources involved in the fittings plan:

    $ python -m plumbery fittings.yaml dispose

## Use case status

- [ ] Work as expected

## See also

- [Web services with plumbery](../)
- [All plumbery fittings plans](../../)

