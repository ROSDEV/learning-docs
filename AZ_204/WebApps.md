# Create Azure App Service Web Apps
* Create an Azure app service Web App
* Enable diagnostic logging
* Deploy code to a web app
* Configure web app settings including SSL, Api, and connection strings
* Implement Auto-Scaling rules, including schedulerd autoscaling and scaling by operations or system metrics

## App Service plans
* Manage the compute power for the entire plan
* Cost and sizing here
* can host multiple app services ( shared plan resources )
* Determine underlying language
* Cannot mix language in a single app service plan

### App service plan
* <u>Shared compute</u>: <b>Free and Shared</b>, the two base tiers, runs an app on the same Azure VM as other App Service apps, including apps of other customers. These tiers allocate CPU quotas to each app that runs on the shared resources, and the resources cannot scale out.
* <u>Dedicated compute</u>: <b>The Basic, Standard, Premium, PremiumV2, and PremiumV3</b> tiers run apps on dedicated Azure VMs. Only apps in the same App Service plan share the same compute resources. The higher the tier, the more VM instances are available to you for scale-out.
* <u>Isolated</u>: <b>This Isolated and IsolatedV2</b> tiers run dedicated Azure VMs on dedicated Azure Virtual Networks. It provides network isolation on top of compute isolation to your apps. It provides the maximum scale-out capabilities.

### What can be in an app service
* Web Apps
* Containers
* Static Sites
* APIs
* Features

## App Services
* Instance of an app
* public facing website link
* Configuration file and settings
* if the app service is in standard or better plan, get slots
* each slot has it own link and configuration, even though part of the samen app service 
* api management can be links to an app service
* CORS infoamtion configured at the app service 
* Scaling UP(More power) bs Scaling OUT(More instances)

### Differences Between Layer 4 and Layer 7 Load Balancing. 
 
<b>Layer 4 load balancing</b> operates at the intermediate transport layer, which deals with delivery of messages with no regard to the content of the messages. Transmission Control Protocol (TCP) is the Layer 4 protocol for Hypertext Transfer Protocol (HTTP) traffic on the Internet. Layer 4 load balancers simply forward network packets to and from the upstream server without inspecting the content of the packets. They can make limited routing decisions by inspecting the first few packets in the TCP stream.

<b>Layer 7 load balancing</b> operates at the high‑level application layer, which deals with the actual content of each message. HTTP is the predominant Layer 7 protocol for website traffic on the Internet. Layer 7 load balancers route network traffic in a much more sophisticated way than Layer 4 load balancers, particularly applicable to TCP‑based traffic such as HTTP. A Layer 7 load balancer terminates the network traffic and reads the message within. It can make a load‑balancing decision based on the content of the message (the URL or cookie, for example). It then makes a new TCP connection to the selected upstream server (or reuses an existing one, by means of HTTP keepalives) and writes the request to the server.