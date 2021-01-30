# Haikoo

![Ansible Lint](https://github.com/oxide-one/haikoo/workflows/Ansible%20Lint/badge.svg)

Because High availability kubernetes on oVirt should be easy, right?

---

# About

Haikoo, short for *High Availability Kubernetes On Ovirt*, is a project to enable the creation and management of production-ready kubernetes clusters on [oVirt](https://www.ovirt.org/). This is enabled through primarily through the use of [Ansible](https://www.ansible.com/).

# Why

In short, because I can.

I built this because I tried out  [Openshift](https://www.openshift.com/) on oVirt and wasn't happy with it for a number of reasons.

**Limitations of Openshift**

- Openshift is incredibly complex

- Openshift uses a lot of power (200w on my cluster)

- It's slow to deploy

With this in mind, I wanted to build my own clusters that were much simpler to understand and work with. I also wanted ones that were easier to maintain without having an entire team behind it. Openshift isn't the answer in this case.

# Project aims

This project does not aim to make kubernetes _easy_. You should know what kubernetes is, and have some basic experience with it. That being said, you could probably go into it without knowing anything about kubernetes and go pretty far.

This project **will** do the following for you:

- Deploy a Kubernetes cluster

- Maintain the number of worker nodes, which involves:

  - Joining nodes to the cluster

  - Removing nodes from the cluster

- Maintain the number of control plane nodes, which involves:

  - Joining control plane nodes to the cluster

  - Removing control plane nodes from the cluster

# Features

The most important feature in this, is the use of [HAProxy](https://www.haproxy.org/) and [Keepalived](https://github.com/acassen/keepalived) to deploy load balanced, fault tolerant control plane nodes.

Each control plane node has an IP address, and shares a Virtual IP address which serves as the control plane endpoint (aka, the kubernetes API). Each node (and you) will connect to this endpoint. This endpoint is served by HAProxy, which distributes load to the rest of the control plane nodes.

In the event that a control plane node goes down, the next control plane node will assume the Virtual IP, and continue operation. Magic stuff really :p
