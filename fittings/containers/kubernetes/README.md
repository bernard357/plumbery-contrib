# Kubernetes node

The objective of this use case is to deploy Kubernetes on a single node, at the [Managed Cloud Platform from Dimension Data](http://cloud.dimensiondata.com/eu/en/).
This is done with [plumbery](https://docs.mcp-services.net/display/PLUM/Plumbery) and a template that is provided below.

Docker is notoriously difficult to deploy in a sophisticated environment. For
example, no routing is provided natively between containers, so you may
have to configure multiple tunnels and address translation rules to deliver
end-to-end connectivity.

By contrast, the ambition of Kubernetes is to leverage the underlying
networking infrastructure, and to provide containers at scale. Well, before
we consider the deployment of hundreds of pods, maybe it would help to start
with a single one, in order to learn.

![Kubernetes deployment](kubernetes.png)

In this tutorial we demonstrate how to create a class of Kubernetes nodes and
deploy one single node. Of course, you can use this file for yourself, and change it
to better accomodate your requirements.


## Requirements for this use case

* Select a MCP location
* Add a Network Domain
* Add an Ethernet network
* Deploy a large Ubuntu server
* Provide 32 CPU and 256 MB of RAM
* Add a virtual disk of 100 GB
* Monitor this server in the real-time dashboard provided by Dimension Data
* Assign a public IPv4 address
* Add address translation to ensure end-to-end IP connectivity
* Add firewall rule to accept TCP traffic on ssh and web ports
* Combine the virtual disks into a single expanded logical volume (LVM)
* Update the operating system of each node
* Synchronise node clock of each node
* Install a new SSH key to secure remote communications
* Configure SSH to reject passwords and to prevent access from root account
* Update `etc/hosts` and `hostnames` to bind IPv6 addresses to host names
* Remove Apache
* Install Go, Docker, Calico and Kubernetes itself

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

Then you can use the Kubernetes controller software to validate the setup:

    $ sudo su
    $ cd /root/kubernetes
    $ cluster/kubectl.sh get services
    $ cluster/kubectl.sh run my-nginx --image=nginx --replicas=2 --port=80
    $ cluster/kubectl.sh get pods

The last command should show the two instances of nginx running.

## Destruction commands

Launch following command to remove all resources involved in the fittings plan:

    $ python -m plumbery fittings.yaml dispose

## Use case status

- [x] Work as expected

## See also

- [Containers with plumbery](../)
- [All plumbery fittings plans](../../)

