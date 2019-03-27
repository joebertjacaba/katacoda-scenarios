You need to be familiar with Networking concepts to be able to be an efficient penetration tester. So if you are not yet familiar, stop now and learn Networking first.

Networking concepts will not be discussed and it is assumed that you have already used or will use that knowledge for discovery.

## Map the network of the system

Here we have different tools at our disposal. One is `traceroute`. The command takes in a hostname or an ip address. It will show the IP addresses of the routers it passes before it reaches a host.

Install it first:

`apt install -y traceroute`{{execute}}

`traceroute katacoda.com`{{execute}}

Another tool is `whois`. It can tell us about ownership and registration information of a domain.

`apt install -y whois`{{execute}}

`whois katacoda.com`{{execute}}

We can use `dig` to query the nameserver of a domain to know where it is hosted.

`dig ns katacoda.com`{{execute}}

There are also many tools available on the web. One of it is cenys.

[censys](https://censys.io/ipv4?q=katacoda.com)

`apt install -y nmap`{{execute}}

*It is not legal in some locations to scan without explicit permission. Proceed with caution.*

Knowing the open ports is a valuable information. We can use `nmap` for this.

`nmap 127.0.0.1`{{execute}}

OpenVAS is an alternative to Nessus since Tenable already commercialized it.

Add the repo:

`add-apt-repository ppa:mrazavi/openvas`{{execute}}

Press <kbd>Enter</kbd>

Update the package lists:

`apt update`{{execute}}

`apt install -y openvas9`{{execute}}

Answer Yes to the Redis question.

You can now see the running openvas services:

`ps -ef | grep openvas | grep -v grep`{{execute}}

Update the vulnerability database:

`greenbone-nvt-sync`{{execute}}

`greenbone-scapdata-sync`{{execute}}

`greenbone-certdata-sync`{{execute}}

Rebuild the database:

`openvasmd --update --verbose --progress`{{execute}}

After the updates we need to restart the necessary services:

`systemctl restart openvas-scanner`{{execute}}

`systemctl restart openvas-manager`{{execute}}

Run the Greenbone Security Assistant Web interface:

`systemctl start openvas-gsa`{{execute}}

Reset the password:

`openvasmd --user=admin --new-password=admin`{{execute}}

Access the web interfae:

https://[[HOST_SUBDOMAIN]]-443-[[KATACODA_HOST]].environments.katacoda.com/