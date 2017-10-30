# Build Microservices and avoid Nanoservices

The whole idea of microservices makes a lot of sense on a highly scalable data pipeline. Using small decoupled services is a sound strategy to build resilient and cost effective systems. When individual services are designed to be nimble and operate as individual nodes, and the service orchestration is on point, the data pipeline will become resilient to unexpected service fails and easy to scale depending on the load.

Decoupled microservices are easier to orchestrate and scaling in/out \[1\] is easier to automate. Having the flexibility to bring services up and down depending on the system load or service malfunction has the potential to make the overall system robust, fail proof and cost effective.

This said the first lesson is that a scalable, robust and cost effective data pipeline must follow a microservice architecture.

But - surprise, surprise! -  there are tradeoffs to consider. Services cannot assume any other service to be running besides itself. From an individual perspective, the service consumes data \(if available\) from some buffer, processes that data and writes the results to another buffer. Message queue services are a great fit for this case and are the nuts and bolts of the decoupling of any microservice architecture. Maintaining a messaging queue service adds some overhead: more resources, maintenance, scalability issues, just to give some examples. Writing and reading from queues needs more time and resources than intra/inter process communication within a single node.

The complexity \(and overhead\) of the system increases proportionally with the number of different services running. Each service needs to consume/publish data from queues, with the associated messaging overhead. Each service needs to publish its own metrics, each service needs to be maintained. And so on. Be careful when defining the boundaries of the services and aim at building a microservice system, not a nanoservices system.

Nanoservices are designed so small that the communication overhead and complexity of the system increase disproportionately to the advantages of having the service decoupled. The logical step is to agglutinate two or more nanoservices together under a single service. While microservices are the basis for a well designed data pipeline, nanoservices will waste resources and increase system complexity unnecessarily. This is a crucial idea to have in mind when designing new features for the pipeline and deciding the service’s boundaries.



**Takeaway**: Design your system as a set of decoupled services. However, be mindful of the overhead introduced by communication and maintenance of multiple services when designing your system. If the communication and sync overhead is too high, agglutinate nanoservices into a single microservice. Avoid nanoservices.



\[1\] scaling in/out \(or horizontally\) means scaling the services by adding or removing nodes to the system. On the other hand, scaling up/down \(or vertically\) means scaling the system by increasing or decreasing the resources of nodes.

