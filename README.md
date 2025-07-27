# Azure Compute Gallery

Instructions how to use Azure Compute Gallery.

First, create an Ubuntu VM.

`az login`

vm_source_rg="ubuntu-source-vm"
location="uksouth"

Create a resource group for the VM:
`az group create --name $vm_source_rg --location $location`

```bash
az vm create \
  --resource-group $vm_source_rg \
  --name ubuntu-source-vm \
  --image Ubuntu2404 \
  --admin-username azureuser \
  --generate-ssh-keys \
  --size Standard_B1s
```

