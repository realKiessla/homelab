# MetalLB
MetalLB is used as a LoadBalancer for our bare metal Kubernetes cluster.

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

### The problem with MetalLB
MetalLB is currently (v0.10.2) not able to provide the functionality described above.
Therefore, we use a customized version of MetalLB which is based on the v0.10.2 which has the still open pull request (PR) [#596](https://github.com/metallb/metallb/pull/596) already merged.

That PR allows us to specify which address pools get announced to which peer.
Before that, MetalLB gave every LoadBalancer all the IPs that she knew of.
So our **internet** LoadBalancer also had the **internal** IP addresses that could not be reached from the internet.

With this PR in place the two LoadBalancers have their respective IP addresses from the correct VLAN assigned.
