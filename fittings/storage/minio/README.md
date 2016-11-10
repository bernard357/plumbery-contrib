# Standalone minio s3-compatible object server

The objective of this use case is to deploy object storage for some development, at the [Managed Cloud Platform from Dimension Data](http://cloud.dimensiondata.com/eu/en/).
This is done with [plumbery](https://docs.mcp-services.net/display/PLUM/Plumbery) and a template that is provided below.

[Minio](https://github.com/minio/minio/blob/master/README.md) is a minimal cloud storage server that is compatible with Amazon S3
APIs. This is useful if you need a lightweight object-based storage backend,
for example while you develop a new digital application.

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
* Add firewall rule to accept TCP traffic on port 22 (ssh) and 8080 (web)
* Combine virtual disks into a single expanded logical volume (LVM)
* Update the operating system
* Synchronise node clock
* Install a new SSH key to secure remote communications
* Configure SSH to reject passwords and to prevent access from root account
* Add minio software and launch the service

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

To actually demonstrate the service you will have to install client
software at your workstation, and configure it to access the back-end.

Minio is compatible with popular S3 tools such as ``s3cmd`` or similar.
Here we will use the Minio client, also called mc.

Instructions to install Minio client software can be found [here](https://github.com/minio/mc)

Next step is to retrieve secrets from the server that has been deployed
by plumbery. To do this you have to connect to the server and to display
a file that was generated during the setup:

    $ ssh root@<ipv4_here>
    ...
    $ cat minio_keys.txt

In a separate terminal window you can paste the AccessKey and the SecretKey
to configure the Minio client:

    $ ./mc config host add http://<public_address>:8080 <AccessKey> <Secretkey>

## Play with the service

Here is the full sequence:
* create a bucket
* copy a file from your workstation to the bucket
* generate a link to retrieve the file securely
* test the link and download the file

In other terms, type this at your workstation:

    $ ./mc mb http://<public_address>:8080/stuff
    $ ./mc cp <file> http://<public_address>:8080/stuff
    $ ./mc share download http://<public_address>:8080/stuff/

A long web link is displayed on last command. Select and copy everything,
then move to a browser window and paste everything in the top bar. Press
Enter to start the download.

You can switch to the other terminal window and check the state of the
server itself:

    $ cd /home/shared
    $ cd stuff
    $ ls

Last command should display the name of the file that you copied earlier
in the sequence.

## Destruction commands

Launch following command to remove all resources involved in the fittings plan:

    $ python -m plumbery fittings.yaml dispose

## Use case status

- [ ] Work as expected

## See also

- [Storage services with plumbery](../)
- [All plumbery fittings plans](../../)

