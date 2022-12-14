---
description: This template deploys a Linux VMSS using the latest Linux image, adds data volumes, and then encrypts the data volumes of each Linux VMSS instance.  It also deploys a jumpbox with a public IP address in the same virtual network as the Linux VMSS instances with private IP addresses.  This allows connecting to the jumpbox via its public IP address, and then connecting to the Linux VMSS instances via private IP addresses.
page_type: sample
products:
- azure
- azure-resource-manager
urlFragment: encrypt-vmss-linux-jumpbox
languages:
- json
---
# Create and encrypt a new Linux VMSS with jumpbox

![Azure Public Test Date](https://azurequickstartsservice.blob.core.windows.net/badges/quickstarts/microsoft.compute/encrypt-vmss-linux-jumpbox/PublicLastTestDate.svg)
![Azure Public Test Result](https://azurequickstartsservice.blob.core.windows.net/badges/quickstarts/microsoft.compute/encrypt-vmss-linux-jumpbox/PublicDeployment.svg)

![Azure US Gov Last Test Date](https://azurequickstartsservice.blob.core.windows.net/badges/quickstarts/microsoft.compute/encrypt-vmss-linux-jumpbox/FairfaxLastTestDate.svg)
![Azure US Gov Last Test Result](https://azurequickstartsservice.blob.core.windows.net/badges/quickstarts/microsoft.compute/encrypt-vmss-linux-jumpbox/FairfaxDeployment.svg)

![Best Practice Check](https://azurequickstartsservice.blob.core.windows.net/badges/quickstarts/microsoft.compute/encrypt-vmss-linux-jumpbox/BestPracticeResult.svg)
![Cred Scan Check](https://azurequickstartsservice.blob.core.windows.net/badges/quickstarts/microsoft.compute/encrypt-vmss-linux-jumpbox/CredScanResult.svg)

[![Deploy to Azure](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/1-CONTRIBUTION-GUIDE/images/deploytoazure.svg?sanitize=true)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fquickstarts%2Fmicrosoft.compute%2Fencrypt-vmss-linux-jumpbox%2Fazuredeploy.json)
[![Deploy To Azure US Gov](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/1-CONTRIBUTION-GUIDE/images/deploytoazuregov.svg?sanitize=true)]( https://portal.azure.us/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fquickstarts%2Fmicrosoft.compute%2Fencrypt-vmss-linux-jumpbox%2Fazuredeploy.json)
[![Visualize](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/1-CONTRIBUTION-GUIDE/images/visualizebutton.svg?sanitize=true)](http://armviz.io/#/?load=https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fquickstarts%2Fmicrosoft.compute%2Fencrypt-vmss-linux-jumpbox%2Fazuredeploy.json)

This template allows you to deploy a simple VM Scale Set of Linux VMs using the latest image version.  This template also deploys a jumpbox with a public IP address in the same virtual network. You can connect to the jumpbox via this public IP address, then connect from there to VMs in the scale set via private IP addresses. This template enables encryption on the VM Scale Set of Linux VMs.

AzureDiskEncryption for VMSS is currently in preview. Consuming this feature requires enabling the preview feature on the subscription and setting up a key vault with 'EnabledForDiskEncryption' access policy using the Azure powershell cmdlets below
1. Register-AzureRmProviderFeature -FeatureName "UnifiedDiskEncryption" -ProviderNamespace "Microsoft.Compute"
2. Set-AzureRmKeyVaultAccessPolicy -ResourceGroupName <rgName> -VaultName <vaultName> -EnabledForDiskEncryption"

__Note: The VMSS encryption preview does not yet support image upgrade or reimage. Do not use this if you will need to upgrade your OS image in an encrypted scale set.__

PARAMETER RESTRICTIONS
======================

vmssName must be 3-61 characters in length. It should also be globally unique across all of Azure. If it isn't globally unique, it is possible that this template will still deploy properly, but we don't recommend relying on this pseudo-probabilistic behavior.
instanceCount must be 100 or less.

`Tags: Microsoft.Network/virtualNetworks, Microsoft.Storage/storageAccounts, Microsoft.Network/publicIPAddresses, Microsoft.Network/networkInterfaces, Microsoft.Compute/virtualMachines, Microsoft.Compute/virtualMachineScaleSets, [variables('extensionName')]`
