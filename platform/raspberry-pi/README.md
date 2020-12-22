# Raspberry Pi
This section contains various information and files about the worker nodes of our CaaS Cluster.

# VLAN
The worker nodes had to be able to connect to two separate (virtual) networks.
One is the internal network, and the other is the internet / DMZ network.

Therefore, VLAN functionality had to be provided for the Raspberry Pi.

## Prerequisite
1. The VLAN package had to be installed:\
`sudo apt install vlan`
1. The `8021q` kernel module had to be added to `/etc/modules` for the module to be added at boot time.

## VLAN Network Interface
The VLAN network interface could be added to our Ubuntu 20.04 LTS with an additional Netplan configuration.
This configuration is stored under [60-vlans.yaml](./vlan/60-vlans.yaml).

It has to be copied to `/etc/netplan/` to configure and enable the VLAN interface.
