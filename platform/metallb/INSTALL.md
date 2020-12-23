# MetalLB Installation
Currently, we are using a customized version of MetalLB 0.9.5.

## Background
At the time of writing this documentation, the current version of MetalLB (0.9.5) did not provide a functionality to limit the announcement of load balancer address pools to specific BGP peers.

That means if we have two VLANs and peers with respectively two LoadBalancers, MetalLB would announce every node of both VLANs to each of the LoadBalancer even when the node address is not in the same VLAN.

For more information regarding this issue read the [README.md](README.md).

## Installation
We only needed to customize the `speaker` of MetalLB, the controller can be used as is.
Therefore, we have to use our own `metallb.yaml` and cannot use the one provided on the website.

- The namespace creation still can be done with:\
`kubectl apply -f https://raw.githubusercontent.com/metallb/metallb/v0.9.5/manifests/namespace.yaml`

- Then we have to apply our customized `metallb.yaml`:\
`kubectl apply -f metallb.yaml`

- On the first installation we also have to generate a secret:\
`kubectl create secret generic -n metallb-system memberlist --from-literal=secretkey="$(openssl rand -base64 128)"`

- Lastly we apply our customized `config.yaml`:\
`kubectl apply -f config.yaml`
