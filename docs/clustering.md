---
layout: docs
title: "Multi-node MicroK8s"
permalink: /docs/clustering
---
# Multi-node MicroK8s

## Adding a node

To create a cluster out of two or more already-running MicroK8s instances,
use the `microk8s.add-node` command. The MicroK8s instance on which this
command is
run will be the master of the cluster and will host the Kubernetes
control plane:

```bash
microk8s.add-node
Join node with: microk8s.join ip-172-31-20-243:25000/DDOkUupkmaBezNnMheTBqFYHLWINGDbf

If the node you are adding is not reachable through the default
interface you can use one of the following:

 microk8s.join 10.1.84.0:25000/DDOkUupkmaBezNnMheTBqFYHLWINGDbf
 microk8s.join 10.22.254.77:25000/DDOkUupkmaBezNnMheTBqFYHLWINGDbf
```

The `add-node` command prints a `microk8s.join` command which should
be executed on the MicroK8s instance that you wish to join to the
cluster:

```bash
microk8s.join ip-172-31-20-243:25000/DDOkUupkmaBezNnMheTBqFYHLWINGDbf
```

Joining a node to the cluster should only take a few seconds. Afterwards
you should be able to see the node has joined:

```bash
microk8s.kubectl get no
```
```no-highlight
NAME               STATUS   ROLES    AGE   VERSION
10.22.254.79       Ready    <none>   27s   v1.15.3
ip-172-31-20-243   Ready    <none>   53s   v1.15.3
```

## Removing a node

To remove a node from the cluster, use `microk8s.remove-node`:

```bash
microk8s.remove-node 10.22.254.79
```

Finally, on the removed node, run `microk8s.leave`. MicroK8s will restart
its own control plane and resume operations as a full single node cluster:

```bash
microk8s.leave
```

<!-- FEEDBACK -->
<div class="p-notification--information">
  <p class="p-notification__response">
    We appreciate your feedback on the docs. You can
    <a href="https://github.com/canonical-web-and-design/microk8s.io/edit/master/docs/clustering.md" class="p-notification__action">edit this page</a>
    or
    <a href="https://github.com/canonical-web-and-design/microk8s.io/issues/new" class="p-notification__action">file a bug here</a>.
  </p>
</div>
