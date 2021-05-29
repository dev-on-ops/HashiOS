# HashiOS
A Live Linux Distribution for Hashicorp Stack private cloud deployments featuring packer build process. The purpose is to provide a live OS that can be pxe booted via BIOS or UEFI and configured at boot to be part of a highly available production ready private cloud leveraging Hashicorp tools and known production ready deployment patterns.


MISC Notes:

For testing with ipxe in basic config:

```
#!ipxe
initrd http://server/hashios_1_0.iso
chain http://server/memdisk iso
```

reference:
https://github.com/mvallim/live-custom-ubuntu-from-scratch
https://itnext.io/how-to-create-a-custom-ubuntu-live-from-scratch-dd3b3f213f81