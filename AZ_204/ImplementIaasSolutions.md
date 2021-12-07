[<- Overview](./README.MD)

# Implement Iaas Solutions

* Provision VMs
* Configure VN for remote access
* Create Arm templates
* Create Container Images for solutions using Docker
* Publish an image to the Azure Container Registry (ACR)
* Run containers by using Azure Container Instance

<br>

* Understand how to do this in the portal 
* Understand Availabilty Zones and Availabilty sets
* Able to di it via PowerShell commands


## VM Sizes
* ### General Purpose <br>
    <i>Balanced CPU to memory Ratio></i>
* ### Compute Optimized
    <i>High CPU to memory ratio</i>
* ### Memory Optimized
    <i>High memory to CPU ratio</i>
* ### Storage Optimized
    <i>High Disk troughput</i>
* ### GPU
    <i>Graphics rendering, model training</i>

## VM Provisioning
* Fault Domains
<i> (Think Metal Racks)</i>
* Availability Sets
(Logical grouping within data center Crosses fault domains)
* Update Domains
(Ability to update these machines at the same time with no downtime)
* Availabilty Zones (Different data centers in the same region, seperate power cooling and networking)

!!!UITZOEKEN Verschil tussen SETS en ZONES

## Arm Templates
https://docs.microsoft.com/nl-nl/azure/azure-resource-manager/templates/overview
* JSON Files
* Declaratie degine what you want Azure makes it happen
* Allows for paramameteruaztion for templates
* All Azure resource can be exported as an Arm template
* Can be nested and Hierachically defined to enfore deployment order
* deploy in parallel when possible to maximize troughput

'DependsOn' prevents early deployment 

