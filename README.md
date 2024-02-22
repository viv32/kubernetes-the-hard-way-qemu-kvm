# Kubernetes The Hard Way on Bare Metal

This tutorial walks you through setting up Kubernetes the hard way. This guide
is not for people looking for a fully automated command to bring up a
Kubernetes cluster. If that's you then check out the
[Getting Started Guides](http://kubernetes.io/docs/getting-started-guides/).

Kubernetes The Hard Way is optimized for learning, which means taking the long
route to ensure you understand each task required to bootstrap a Kubernetes
cluster.

> [!NOTE]
> The results of this tutorial should not be viewed as production ready, and
may receive limited support from the community, but don't let that stop you
from learning!

## Copyright

<a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-sa/4.0/88x31.png" /></a><br />This work is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/">Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License</a>.

## Differences with the original kubernetes-the-hard-way and others

> [!NOTE]
> This tutorial has been forked from [Kubernetes The Hard Way (Libvirt KVM edition)](https://github.com/alosadagrande/kubernetes-the-hard-way-libvirt-kvm) written by Alberto Losada which is itself a fork of the esteemed [Kubernetes The Hard Way](https://github.com/kelseyhightower/kubernetes-the-hard-way) by Kelsey Hightower. I also referenced [Kubernetes The Hard Way - Proxmox (KVM)](https://github.com/DushanthaS/kubernetes-the-hard-way-on-proxmox/tree/master) from DushanthaS when updating this guide. Specials thanks to all three.

The main difference is that instead of running our cluster on top of an IaaS solution as Google Cloud or OpenStack, we aim to deploy a Kubernetes cluster on a baremetal server. We will leverage the virtualization capabilities that comes with GNU/Linux (libvirt/KVM/QEMU) to easily provide a similar *virtual infrastructure*. Note that in this case, we could use any spare baremetal server or laptop (with enough resources) running a GNU/Linux distribution.

Some other differences in this installation against the original one:

- Dedicated instance for load balancing (with HAProxy).
- My own personal flair

## Target Audience

The target audience for this tutorial is someone planning to support a
production Kubernetes cluster and wants to understand how everything fits
together.

## Cluster Details

Kubernetes The Hard Way guides you through bootstrapping a highly available
Kubernetes cluster with end-to-end encryption between components and RBAC
authentication.

- [Kubernetes](https://github.com/kubernetes/kubernetes) 1.29.1
- [containerd Container Runtime](https://github.com/containerd/containerd) 1.7.13
- [coredns](https://github.com/coredns/coredns) v1.11.1
- [cni-plugins](https://github.com/containernetworking/plugins) v1.4.0
- [etcd](https://github.com/coreos/etcd) v3.5.12

## Labs

This tutorial assumes you have access to a Pop!_OS hist you can use to run virt-manager. Your machine should have 25GB unused RAM and 140GB free HDD/SSD Storage. While I use Pop!_OS for this tutorial you could easily follow along with any other linux distros, even a headless server if you are more familiar with kvm.

- [Prerequisites](docs/01-prerequisites.md)
- [Installing the Client Tools](docs/02-client-tools.md)
- [Provisioning Compute Resources](docs/03-compute-resources.md)
- [Provisioning the CA and Generating TLS Certificates](docs/04-certificate-authority.md)
- [Generating Kubernetes Configuration Files for Authentication](docs/05-kubernetes-configuration-files.md)
- [Generating the Data Encryption Config and Key](docs/06-data-encryption-keys.md)
- [Bootstrapping the etcd Cluster](docs/07-bootstrapping-etcd.md)
- [Bootstrapping the Kubernetes Control Plane](docs/08-bootstrapping-kubernetes-controllers.md)
- [Bootstrapping the Kubernetes Worker Nodes](docs/09-bootstrapping-kubernetes-workers.md)
- [Configuring kubectl for Remote Access](docs/10-configuring-kubectl.md)
- [Provisioning Pod Network Routes](docs/11-pod-network-routes.md)
- [Deploying the DNS Cluster Add-on](docs/12-dns-addon.md)
- [Smoke Test](docs/13-smoke-test.md)
- [Cleaning Up](docs/14-cleanup.md)
