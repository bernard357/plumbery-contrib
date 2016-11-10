# MySQL replication over IPv6 back-end network

The objective of this use case is to deploy a MySQL server and a MySQL client at two different locations, at the [Managed Cloud Platform from Dimension Data](http://cloud.dimensiondata.com/eu/en/).
This is done with [plumbery](https://docs.mcp-services.net/display/PLUM/Plumbery) and a template that is provided below.

In this use case a master database server and a slave database server are
deployed in different locations. The back-end IPv6 infrastructure
provided by Dimension Data is used to replicate data continuously and securely.

As shown below, plumbery provides a streamlined definition of the overall
solution, that encompasses servers location, the networking infrastructure,
the security of information flows, but also the contextualisation of nodes
and the small but important final brushes that are making a solution really
appealing.

When starting from scratch, it takes about 15 minutes to deploy the fittings plan
below. About half of it is related to the deployment at cloud services from
Dimension data. The other half is incurred by cloud-init in the contextualisation
of nodes, the software part of the solution.
After that time, you can connect to the cluster and use it for real.

## Requirements for this use case

* Select two MCP locations
* Add a Network Domain at each location
* Add an Ethernet network at each location
* Allow IPv6 traffic between the two networks
* Deploy a Ubuntu server at each location
* Monitor these servers in the real-time dashboard provided by Dimension Data
* Provide 8 CPU and 32 GB of RAM to each node
* Add a virtual disk of 50 GB to each node
* Assign public IPv4 addresses to nodes
* Add address translation to ensure end-to-end IP connectivity
* Add firewall rule to accept TCP traffic on port 22 (ssh)
* Combine virtual disks into a single expanded logical volume (LVM)
* Update the operating system of each node
* Synchronise nodes clock with NTP
* Install a new SSH key to secure remote communications
* Configure SSH to reject passwords and to prevent access from root account
* Add IPv6 addresses to `/etc/hosts` for easy handling
* Install MySQL at each node
* Configure the master database
* Configure the slave database
* Populate the master database
* Dump the master database and load it at the slave node
* Start the replication from the master to the slave

## Fittings plan

The plan below demonstrates multiple interesting building blocks:

* Addition of public IPv4 and firewall rules to control access to
  selected servers
* Configuration of the firewall to open communications across data centres
* Automatic registration to the monitoring services provided by Dimension Data
* Management of SSH keys to enable secured communications without passwords
* Update of etc/hosts with IPv6
* Easy templating of configuration files transmitted to nodes
* Handy generation and management of secrets required at various places
* rsync on top of ipv6 to manage heavy communications between servers
* User documentation of the infrastructure is put directly in the fittings plan

[Click here to read fittings.yaml](fittings.yaml)

## Deployment command

In this case, the blueprint ``sql`` is spread over two different
data centres. For this reason, plumbery will connect separately
to each data centre and to the dirty job to make you happy.

    $ python -m plumbery fittings.yaml deploy

This command will build fittings as per the provided plan, start the server
and bootstrap it. Look at messages displayed by plumbery while it is
working, so you can monitor what's happening.

## Follow-up commands

At the end of the deployment, plumbery will display on screen some instructions
to help you move forward. You can ask plumbery to display this information
at any time with the following command:

    $ python -m plumbery fittings.yaml information

Since servers are up and running, you are invited to play a bit with them, and
show evidence of data replication. For example, you could open two additional
terminal windows, one for the master server and the other for the slave server.
Then connect by ssh, using the ubuntu account, and enter mysql directly.

    $ ssh ubuntu@<node_ipv4>
    $ mysql

On the master side, you can type these commands in sequence:

    use db01;
    select * from persons;
    show master status \G

Then move to the slave side, and check status of the server:

    use db01;
    select * from persons;
    show slave status \G

At this stage, the slave server should report the same GTID index than the
master.

Move back to the master server, and create a new record in the table:

    insert into persons (name) values ('Alfred');
    show master status \G

The last command should show a progress in the GTID information. How is this
reflected on slave side? There you can type the following:

    select * from persons;
    show slave status \G

The SELECT statement should reflect the record created on the other side. And
the SHOW statement should follow the evolution of the GTID on the master side.

## Troubleshooting

The fittings plan is using multiple secrets, and most of them have been used
by plumbery to configure the solution dynamically. If you need to retrieve
one of these secrets, for example, the root password for SQL, then use the
following command:

    $ python -m plumbery fittings.yaml secrets

## Destruction commands

Launch following command to remove all resources involved in the fittings plan:

    $ python -m plumbery fittings.yaml dispose

## Use case status

- [ ] Work as expected

## See also

- [Storage services with plumbery](../)
- [All plumbery fittings plans](../../)

