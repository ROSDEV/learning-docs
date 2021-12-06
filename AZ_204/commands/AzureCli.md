# Overview of Azure Cli Commands 

Create AZ Group<br>
```
az group create --name myResourceGroup --location eastus
```
Create VM 
```
az vm create 
--resource-group myResourcegroup
--name myVmName
--image win2019datacenter
--size Standard_D2s_v3
--admin-username azureuser
```

Create AppService plan 
```
myGroup=my-testing-group
myLocation=centralus
myPlan=my-service-plan

az group create --name $myGroup --location $myLocation

az appservice plan create \
        --name $myPlan \
        --resource-group $myGroup \
        --sku S1
```
Deploy Application to an Azure app Service
```
myPlan=my-service-plan
myAppName=simple-web-app
myGroup=my-testing-group

az webapp create \
    --name $myAppName \
    --plan $myPlan \
    --resource-group $myGroup
```