# Hubot server

[Hubot](https://hubot.github.com) is a software robot written in CoffeeScript on Node.js.
It's designed to automate company chat room.

![hubot](hubot.png)

In this use case we demonstrate how to create a ready-to-use Hubot server
on a single node at the [Managed Cloud Platform from Dimension Data](http://cloud.dimensiondata.com/eu/en/).
This is done with [plumbery](https://docs.mcp-services.net/display/PLUM/Plumbery) and a template that is provided below.

## Requirements for this use case

* Go to a MCP location
* Add a Network Domain
* Add an Ethernet network
* Deploy a Ubuntu server
* Provide enough CPU and RAM
* Add a virtual disk
* Monitor this server in the real-time dashboard
* Assign a public IPv4 address
* Add address translation to ensure end-to-end IP connectivity
* Add firewall rule to accept TCP traffic on port 22 (ssh)
* Use the virtual disk to expand logical volume (LVM)
* Update the operating system
* Synhronise node clock
* Edit the host name and the `/etc/hosts` file
* Install a new SSH key to secure remote communications
* Configure SSH to reject passwords and to prevent access from root account
* Install Nodejs, npm and hubot itself
* Create a bot
* Add some pre-existing scripts to the bot

## Fittings plan

[Click here to read fittings.yaml](fittings.yaml)

## Deployment command

    $ python -m plumbery fittings.yaml deploy

This command will build fittings as per the provided plan, start the server
and bootstrap it.

## Follow-up commands

You can find the public address assigned to the Let's Chat node like this:

    $ python -m plumbery fittings.yaml information

Use ssh to connect to the server

    $ ssh ubuntu@<public-ip-address>

From there, you can launch hubot from the command line and play with it
interactively.

    $ cd plum
    $ bin/hubot
    > plum help

## Destruction commands

Launch following command to remove all resources involved in the fittings plan:

    $ python -m plumbery fittings.yaml dispose

## Use case status

- [x] Work as expected

## See also

- [Collaboration services with plumbery](../)
- [All plumbery fittings plan](../../)

