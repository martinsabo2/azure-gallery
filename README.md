# Azure Compute Gallery

Instructions how to use Azure Compute Gallery.

First, create an Ubuntu VM.

`az login`

`vm_source_rg="ubuntu-source-vm"`
`location="uksouth"`

Create a resource group for the VM:
`az group create --name $vm_source_rg --location $location`

```bash
az vm create \
  --resource-group $vm_source_rg \
  --name ubuntu-source-vm \
  --image "canonical:0001-com-ubuntu-minimal-jammy:minimal-22_04-lts-gen2:latest" \
  --admin-username azureuser \
  --generate-ssh-keys \
  --size Standard_B1s
```
Log into the machine and run:

`sudo waagent -deprovision+user`
and shutdown the VM.

Deallocate the VM: 
`az vm deallocate --resource-group <rg> --name <vm-name>`

Generalize the VM:
`az vm generalize --resource-group <rg> --name <vm-name>`

Create a Managed Image from the VM:
- warning: Creation of managed images are not supported for virtual machine with TrustedLaunch security type.
```bash
az image create \
  --resource-group <rg> \
  --name myUbuntuImage \
  --source <vm-name> \
  --os-type Linux
```
Create a Shared Image Gallery:
```bash
az sig create \
  --resource-group <rg> \
  --gallery-name myGallery \
  --location <region>
```
