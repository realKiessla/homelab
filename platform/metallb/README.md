# MetalLB
MetalLB is used as a LoadBalancer for our bare metal Kubernetes cluster.

## Installation
Before the MetalLB templates (this Helm Chart) can be installed, the MetalLB components and CRDs have to be manually deployed before:
```
kubectl apply -f https://raw.githubusercontent.com/metallb/metallb/v0.13.4/config/manifests/metallb-native.yaml
```

## Configuration
MetalLB is configured to provide two LoadBalancers (IPs) for our two ingresses.

```
+-------------+            +---Kubernetes Cluster------------------+
| Internet LB |            |    +-------------+    +-------------+ |
|  (MetalLB)  +------------+----+   Ingress   +----+   Service   | |
+-------------+            |    +-------------+    +-------------+ |
                           |                                       |
+-------------+            |    +-------------+    +-------------+ |
| Intranet LB +------------+----+   Ingress   +----+   Service   | |
|  (MetalLB)  |            |    +-------------+    +-------------+ |
+-------------+            +---------------------------------------+
```

**Description**\
Our network consists of two separate virtual networks (VLAN), the intranet (CAAS) and the internet (DMZ).
In each of those two networks we want to run one LoadBalancer which can balance the incoming traffic between our nodes.

We currently have three Kubernetes nodes. Each node is in both VLANs.
So each node has 2 IP addresses but only one can be reached from the respective LoadBalancer.

With that we have a good separation between the internal, and the internet network while having the freedom of choice from where our service is reachable.
