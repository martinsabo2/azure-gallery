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
`sudo shutdown -h now`


