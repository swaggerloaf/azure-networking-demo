# azure-networking-demo
An Azure networking demo


<code>
az login
az account --help
az account list
az account set --subscription <sub id>
</code>

<code>
az network vnet create \
    --resource-group learn-81f90fe2-afdc-4ca0-9f6d-48d381bdb382 \
    --name SalesVNet \
    --address-prefix 10.1.0.0/16 \
    --subnet-name Apps \
    --subnet-prefix 10.1.1.0/24 \
    --location northeurope
</code>

<code>
az network vnet create \
    --resource-group learn-81f90fe2-afdc-4ca0-9f6d-48d381bdb382 \
    --name ResearchVNet \
    --address-prefix 10.3.0.0/16 \
    --subnet-name Data \
    --subnet-prefix 10.3.1.0/24 \
    --location westeurope
</code>
