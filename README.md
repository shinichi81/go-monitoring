# go-monitoring

Let’s sum this all up by creating a list of all layers and the parts of our software therein:

├── delivery            // Serve content via HTTP? CLI? everything related to that should be here
|
├── domain              // Where we have our domain logic
|
├── infrastructure      // Where we have our implementation details (Database connections, Queues, External services)
|
└── usecase             // The glue between our delivery layer and our domain layer. Different
                        // Delivery mechanisms probably will have the same use cases or very similiar
                        // use cases, this allows you to use the same code for different mechanisms by
                        // using the same use case interactors in different mechanisms
