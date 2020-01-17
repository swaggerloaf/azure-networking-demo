# azure-networking-demo
An Azure networking demo


```
az login
az account --help
az account list
az account set --subscription <sub id>
```

```
az network vnet create \
    --resource-group learn-81f90fe2-afdc-4ca0-9f6d-48d381bdb382 \
    --name SalesVNet \
    --address-prefix 10.1.0.0/16 \
    --subnet-name Apps \
    --subnet-prefix 10.1.1.0/24 \
    --location northeurope
```

```
az network vnet create \
    --resource-group learn-81f90fe2-afdc-4ca0-9f6d-48d381bdb382 \
    --name ResearchVNet \
    --address-prefix 10.3.0.0/16 \
    --subnet-name Data \
    --subnet-prefix 10.3.1.0/24 \
    --location westeurope
```

```
az network vnet create \
    --resource-group learn-81f90fe2-afdc-4ca0-9f6d-48d381bdb382 \
    --name ResearchVNet \
    --address-prefix 10.3.0.0/16 \
    --subnet-name Data \
    --subnet-prefix 10.3.1.0/24 \
    --location westeurope
```

Configured peering connections between the virtual networks to enable resources to communicate with each other. Your configuration used a hub and spoke topology. MarketingVNet was the hub, and SalesVNet and ResearchVNet were spokes.



```
az network vnet list --output table
```

```
az vm create \
    --resource-group learn-81f90fe2-afdc-4ca0-9f6d-48d381bdb382 \
    --no-wait \
    --name SalesVM \
    --location northeurope \
    --vnet-name SalesVNet \
    --subnet Apps \
    --image UbuntuLTS \
    --admin-username azureuser \
    --admin-password <password>
```

```
az vm create \
    --resource-group learn-81f90fe2-afdc-4ca0-9f6d-48d381bdb382 \
    --no-wait \
    --name MarketingVM \
    --location northeurope \
    --vnet-name MarketingVNet \
    --subnet Apps \
    --image UbuntuLTS \
    --admin-username azureuser \
    --admin-password <password>
 ```
 
 
 ```
 az vm create \
    --resource-group learn-81f90fe2-afdc-4ca0-9f6d-48d381bdb382 \
    --no-wait \
    --name ResearchVM \
    --location westeurope \
    --vnet-name ResearchVNet \
    --subnet Data \
    --image UbuntuLTS \
    --admin-username azureuser \
    --admin-password <password>
```

```
az vm list \
    --resource-group learn-81f90fe2-afdc-4ca0-9f6d-48d381bdb382 \
    --show-details \
    --query '[*].{Name:name, ProvisioningState:provisioningState, PowerState:powerState}' \
    --output table
```

```
az network vnet peering create \
    --name SalesVNet-To-MarketingVNet \
    --remote-vnet MarketingVNet \
    --resource-group learn-81f90fe2-afdc-4ca0-9f6d-48d381bdb382 \
    --vnet-name SalesVNet \
    --allow-vnet-access
```
 
```
az network vnet peering create \
    --name MarketingVNet-To-SalesVNet \
    --remote-vnet SalesVNet \
    --resource-group learn-81f90fe2-afdc-4ca0-9f6d-48d381bdb382 \
    --vnet-name MarketingVNet \
    --allow-vnet-access
```


```
az network vnet peering create \
    --name MarketingVNet-To-ResearchVNet \
    --remote-vnet ResearchVNet \
    --resource-group learn-81f90fe2-afdc-4ca0-9f6d-48d381bdb382 \
    --vnet-name MarketingVNet \
    --allow-vnet-access
```

```
az network vnet peering create \
    --name ResearchVNet-To-MarketingVNet \
    --remote-vnet MarketingVNet \
    --resource-group learn-81f90fe2-afdc-4ca0-9f6d-48d381bdb382 \
    --vnet-name ResearchVNet \
    --allow-vnet-access
```


```
az network vnet peering list \
    --resource-group learn-81f90fe2-afdc-4ca0-9f6d-48d381bdb382 \
    --vnet-name SalesVNet \
    --output table
```

```
az network nic show-effective-route-table \
    --resource-group learn-81f90fe2-afdc-4ca0-9f6d-48d381bdb382 \
    --name SalesVMVMNic \
    --output table
```

```
az vm list \
    --resource-group learn-ef2246dc-435d-4abf-aba2-e7f908323888 \
    --query "[*].{Name:name, PrivateIP:privateIps, PublicIP:publicIps}" \
    --show-details \
    --output table
```

```
ssh -o StrictHostKeyChecking=no azureuser@<SalesVM public IP>
```

```
ssh -o StrictHostKeyChecking=no azureuser@<ResearchVM private IP>
```
