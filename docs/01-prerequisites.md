# Prerequisites

## Virtualization platform
This tutorial leverages libvirt and KVM/QEMU to streamline provisioning of the compute infrastructure required to bootstrap a Kubernetes cluster from the ground up. I provide instructions here for the virt-manager GUI but CLI tools can be used also in a headless environment. Instructions for this can be found in the upstream [Kubernetes The Hard Way (Libvirt KVM edition)](https://github.com/alosadagrande/kubernetes-the-hard-way-libvirt-kvm)

In my case, I use a Lenovo ThinkCentre m920q with a fresh install of Pop!_OS. Any distro with a graphical user interface should do just fine.

```
Host: k8s-lab
Processor: Intel® Core™ i5-8500T CPU @ 2.10GHz × 6 
Memory: 32.0 GiB
Storage: 512 GB SSD	
```

During this tutorial we will configure a high availability Kubernetes cluster made  up of the following virtual machines on bare metal.

|  VM Name      | Purpose    |   OS     | vCPUs | Memory | Disk  |
| ------------- | ---------- | ---------|-------|--------|-------|
| controller-01 | controller | Ubuntu   |   2   |  4 GB  | 20 GB |
| controller-02 | controller | Ubuntu   |   2   |  4 GB  | 20 GB |
| controller-03 | controller | Ubuntu   |   2   |  4 GB  | 20 GB |
| worker-01     | controller | Ubuntu   |   2   |  4 GB  | 20 GB |
| worker-02     | controller | Ubuntu   |   2   |  4 GB  | 20 GB |
| worker-03     | controller | Ubuntu   |   2   |  4 GB  | 20 GB |
| gateway-01    | balancer   | Ubuntu   |   1   |  2 GB  | 20 GB |

If you're not familiar with this level of the virtualization stack, the total vCPUs of the virtual machines exceeding what my machine has available might be confusing. Most of the time, CPU resources are not fully utilized by the virtual machines and can thus be overcommitted to other VMs. If all VMs need their full usage of the CPUs, they get slowed down and forced to share the limited compute resources. Memory can be similarly overcommitted, but if the VMs use more memory than is actually available on the host machine, things get ugly. Swap space on disk is used causing a severe performance degradation or the host OS may force the VMs to close. 
> [!TIP]
> My general rule of thumb: overcommit CPUs freely, avoid overcommitting memory when possible.

## Installing the virtualization platform onto the host

Install the primitives:
```
sudo apt-get install qemu-system qemu-system-x86 qemu-utils qemu-kvm
```
Install the GUI:
```
sudo apt-get install virt-manager
```
Finally, start and enable the systemd service:
```
systemctl enable libvirtd --now
```
## Creating your first VM with virt-manager.
Launch virt-manager _(Virtual Machine Manager)_. If it cannot connect to QEMU/KVM, you may need to restart your system.

For simplicity and familiarity sake I use Ubuntu Server 22.04 for all the virtual machines in this tutorial. You can use something else if you prefer.

1. Go to `File > New Virtual Machine`
2. Select `Local Install Media`
3. Select your ISO
4. Give your VM `4096 KiB Memory` and `2 CPUs`
5. Give a `20 GiB` virtual disk.
> [!NOTE]
> By default, virtual disks for your virtual machines are stored at `/var/lib/libvirt/images`
6. Name your virtual machine `controller-01`
> [!IMPORTANT]
> libvirt creates a default network for VMs, `192.168.122.0/24`. We will use this for our nodes.
7. Click Finish. Your virtual machine will begin running! You should close it and power it off for now though.

## Running Commands in Parallel with tmux

[tmux](https://github.com/tmux/tmux/wiki) can be used to run commands on multiple compute instances at the same time. Labs in this tutorial may require running the same commands across multiple compute instances, in those cases consider using tmux and splitting a window into multiple panes with `synchronize-panes` enabled to speed up the provisioning process.

> The use of tmux is optional and not required to complete this tutorial.

![tmux screenshot](images/tmux-screenshot.png)

> Enable synchronize-panes by pressing `ctrl+b` followed by `shift+:`. Next type `set synchronize-panes on` at the prompt. To disable synchronization: `set synchronize-panes off`.

There are other options, the most remarkable in my opinion is [terminator](https://terminator-gtk3.readthedocs.io/en/latest/) which I use a lot.

Next: [Installing the Client Tools](02-client-tools.md)
