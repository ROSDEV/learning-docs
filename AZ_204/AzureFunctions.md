

[<- Overview](./README.MD)

## Azure Functions
What is Azure Functions: (from Microsoft Azure) is a cloud-based serverless service that allows running event-triggered code in a scalable way without providing or managing infrastructure. It enables the capability to run a script or piece of code in response to a variety of events and doesn’t need to run continuously.

* Implement input and ouput binding for a function
* Implement function triggers by usings data operations, timers and webhooks
* Implement Azure Durable functions

## Function bindings
Know the difference between 
* Trigger (Example HTTP trigger,Timer trigger, Azure Blob Storage trigger, Azure Event Grid trigger)
* Input binding ( Example Storage Account, Azure Cosmos DB , Third-Party Apps)
* Output binding ( Example Storage Account, Azure Cosmos DB , Third-Party Apps)

<br>
 * Every function has one trigger and optional bindings.
 * An input binding is the data that your function receives. An output binding is the data that your function sends

# Durable Functions
* Originally Functions were Stateless. by default they still are
* Durable functions allow for statefull programming
* Persists across time - has to be manually cleared
* Durable ( Statefull ) entitites
* Durable Orchestrations
* Applications patterns 
    * Chaining
    * Fanning
    * Async
    * Monitoring
    * Human interaction
    * Aggregator



