# HashiOS
A Live Linux Distribution for Hashicorp Stack private cloud deployments featuring packer build process. The purpose is to provide a live OS that can be pxe booted via BIOS or UEFI and configured at boot to be part of a highly available production ready private cloud leveraging Hashicorp tools and known production ready deployment patterns.


MISC Notes:

For testing with ipxe in basic config:

```
#!ipxe
dhcp
set base-url http://192.168.255.101/
kernel ${base-url}hashios-vmlinuz \
boot=ramdisk \
ramroot=http://192.168.255.101/hashios-root.tar.xz \
BOOTIF=01-${netX/mac:hexhyp}
initrd ${base-url}hashios-initrd.img
boot
```

Deployment architecture:
# base location management plane, manages location control planes
1 x git server (virtual) | stores git repos with configurations
1 x vault server (virtual) | stores root secrets
1 x nomad server (physical)| runs management jobs for location clusters terraform, packer
    # workloads:
    terraform workers
    vault server
# baremetal management plane, manages servers for running workloads
3-5 x nomad servers (physical) | used to run management workloads
3-5 x vault servers (virtual) | stores servers for location and dynamic secret engines
3-5 x consul servers (virtual) | distributed key value store, dns interfaces, service registry
3-5 x nomad servers (virtual) | schedules jobs on cluster nodes and terraform runs terrafrom, packer and applicaiton jobs
0-100 x nomad / consul workers (physical) | application workloads scheduled here
    # workloads:
    git replicas
    terraform workers
# per location management plane, manages servers for running workloads
3-5 x vault servers | stores servers for location and dynamic secret engines
3-5 x consul servers | distributed key value store, dns interfaces, service registry
3-5 x nomad servers | schedules jobs on cluster nodes and terraform runs terrafrom, packer and applicaiton jobs
0-100 x nomad / consul workers | application workloads scheduled here
    # workloads:
    git replicas
    terraform workers