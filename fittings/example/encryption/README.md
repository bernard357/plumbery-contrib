# Encryption of data disk with LUKS and LVM

The objective of this use case is to deploy a server with encrypted storage, at the [Managed Cloud Platform from Dimension Data](http://cloud.dimensiondata.com/eu/en/).
This is done with [plumbery](https://docs.mcp-services.net/display/PLUM/Plumbery) and a template that is provided below.

[Linux Unified Key Setup (LUKS)](https://gitlab.com/cryptsetup/cryptsetup/blob/master/README.md) is a disk encryption specification. Over time it has become a platform-independent standard on-disk format for use in various tools. This not only facilitates compatibility and interoperability among different programs, but also assures that they all implement password management in a secure and documented manner.

![LUKS](luks.png)

In this use case we add an encrypted virtual disk by providing a passphrase.
The password is required on each reboot to access encrypted data. Without it,
protected data cannot be retrieved.

## Requirements for this use case

* Select a MCP location
* Add a Network Domain
* Add an Ethernet network
* Deploy a CentOS node
* Add disk 1 with 10 GB of standard storage
* Monitor this server in the real-time dashboard provided by Dimension Data
* Assign a public IPv4 address
* Add address translation to ensure end-to-end IP connectivity
* Add firewall rule to accept TCP traffic on port 22 (ssh)
* Partition the additional disk
* Update the operating system
* Synchronise node clock with NTP
* Install a new SSH key to secure remote communications
* Configure SSH to reject passwords and to prevent access from root account
* Generate a random passphrase
* Use LUKS to encrypt the new partition
* Use LVM to manage logical storage
* Create new mount /crypted to expose the new encrypted disk
* Configure /etc/fstab to remember the configuration
* Write a sample file on encrypted disk
* Reboot the node to close the encrypted disk

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

    $ ssh centos@<ipv4_here>

You will have to accept the new host, and authentication will be based on
the SSH key communicated to the node by Plumbery.

    $ sudo su
    # cat /crypted/welcome.txt

This command should report an error, since the encrypted disk has not been mounted.

    # echo -n <secret_passphrase_here> | cryptsetup luksOpen /dev/sdb sdb_crypt -
    # mount /crypted
    # cat /crypted/welcome.txt

These commands show how to mount the encrypted disk and to read content. This
has to be done each time the server is rebooted.

![screenshot](screenshot.png)

The secret is not stored on the node itself, but on plumbery side. To retrieve it, type the following command:

    $ python -m plumbery fittings.yaml secrets

## Destruction commands

Launch following command to remove all resources involved in the fittings plan:

    $ python -m plumbery fittings.yaml dispose

## Use case status

- [X] Work as expected

## See also

- [Example configurations with plumbery](../)
- [All plumbery fittings plans](../../)

