# Packer bare metal

This repository lets you create a minimalistic Ubuntu 20.04 vmdk via packer and then use it to install OS on a bare metal server. 

## how it works? 

- `virtualbox-iso` builder is used to generate a vmdk. 
- Compress post-processor is used to generate a tar ball and keep the artifacts. 
- `pressed.cfg` in http directory automates the deployment and required configuration. 
- Once the packer process is completed, end result is a vmdk and tar file. 
- vmdk is separately comverted to rawimage format and compressed to generate a gz file.
- This raw or gz file then can be separetly used for provisioning OS.
- Here we would be using The [Tinkerbell](https://docs.tinkerbell.org/) for provisioning of the OS and bare-metal server would be emulated via a Vagrant VM with virtualbox provider. Alternatively, the raw or gz can be mounted on a disk and boot process can be managed via `/etc/fstab`. 
- Follow references for more details.

## steps to be followed

```
PACKER_LOG=1 packer build config.json 
qemu-img convert -f vmdk -o raw output-virtualbox-iso/packer-ubuntu-64-20.04-disk001.vmdk test_packer.raw 
gzip test_packer.raw
```
Refrences:
- https://www.packer.io/docs/
- https://www.packer.io/docs/post-processors/compress
- https://help.ubuntu.com/community/Fstab




