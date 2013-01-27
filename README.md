Description
===========
Install and configure a DHCP3 server, optionally configuring it to automatically
register hosts with a Bind9 name server.

Requirements
============
Ubuntu. Other platforms were not tested.

Attributes
==========
+ `domain` - The domain name to update.
+ `subnets` - Subnets to use for allocating IP addresses. See example below.
+ `subnet` - A specific subnet from `subnets` to use on this node.
+ `conf_dif` - Location to place configuration files (defaults to `/etc/dhcp3`).

Usage
=====
The `subnets` attribute needs to describe a subnet to alloacate IP addresses
from, like this:

    "subnets": {
        "secure": {
            "network": "10.1.0.0",
            "netmask": "255.255.0.0",
            "broadcast": "10.1.255.255",
            "range_start": "10.1.13.50",
            "range_end": "10.1.255.200",
            "router": "10.1.0.1",
            "iface": "eth0"
        },
        "dmz": {
            "network": "10.2.0.0",
            "netmask": "255.255.0.0",
            "broadcast": "10.2.255.255",
            "range_start": "10.2.14.1",
            "range_end": "10.2.255.200",
            "router": "10.2.0.1",
            "iface": "eth0"
        }
    }

Additionally, a zone file similar to the one used by the Bind9 cookbook is
needed, with the following attributes under the domain name matching the DHCP
node's domain attribute:

    "dhcp": {
        "ttl": 60,
        "lease-time": 3600,
        "max-lease-time": 3600
    }

TODO
====
+ `subnets` is currently expected to be found on the node itself, leading to it
  being placed on the environment (as a default attribute). Need to change it to
  be read from a separate data bag item.

License and Author
==================

Author:: Leeor Aharon (<leeor@cloudshare.com>)

Copyright 2013 CloudShare, Inc.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
