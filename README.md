# Clean Architecture in Go

An example of "Clean Architecture" in Go to demonstrate developing a testable
application that can be run on AppEngine with Google Cloud Storage or with
traditional hosting and MongoDB for storage (but not limited to either).

There are a number of different application architectures that are all simlar
variations on the same theme which is to have clean separation of concerns and
dependencies that follow the best practices of "the dependency invesion principle":

A. High-level modules should not depend on low-level modules. Both should depend on abstractions.

B. Abstractions should not depend on details. Details should depend on abstractions.

Variations of the approach include:

* [The Clean Architecture](https://blog.8thlight.com/uncle-bob/2012/08/13/the-clean-architecture.html) advocated by Robert Martin ('Uncle Bob')
* Ports & Adapters or [Hexagonal Architecture](http://alistair.cockburn.us/Hexagonal+architecture) by Alistair Cockburn
* [Onion Architecture](http://jeffreypalermo.com/blog/the-onion-architecture-part-1/) by Jeffrey Palermo

From more in-depth practical application of many of the ideas I can strongly
recommend the excellent book [Implementing Domain-Driven Design](http://www.amazon.com/Implementing-Domain-Driven-Design-Vaughn-Vernon/dp/0321834577)
by Vaughn Vernon that goes into far greater detail.

_Source: The Clean Architecture_

![Clean Architecture](docs/go-cleanarch.png)


## Project schema requirements

go-monitoring assumes this files structure:

    [GOPATH]/[PACKAGE_NAME]/[LAYER_NAME]

or

    [GOPATH]/[PACKAGE_NAME]/[MODULE_NAME]/[LAYER_NAME]


for this monitoring-alert, we will use 4 layer :

### Models Layer

This layer is a layer that will save the model in use on the domain and other domains.
This layer can be accessed by all layers and by all domains

Same as Entities, will used in all layer. This layer, will store any Object’s Struct and it’s method. 
Example : Article, Student, Book.

### Repository Layer
Repository will store any Database handler. Querying, or Creating/ Inserting into any database will stored here. This layer will act for CRUD to database only. No business process happen here. Only plain function to Database.
This layer also have responsibility to choose what DB will used in Application. Could be Mysql, MongoDB, MariaDB, Postgresql whatever, will decided here.
If using ORM, this layer will control the input, and give it directly to ORM services.
If calling microservices, will handled here. Create HTTP Request to other services, and sanitize the data. This layer, must fully act as a repository. Handle all data input - output no specific logic happen.
This Repository layer will depends to Connected DB , or other microservices if exists..

### Use Case Layer
This layer will serve as a controller, where the task is to win business logic on every domain.
This layer also has the task of selecting what repository to use, and this domain can have more than one repository layer
The biggest main task of this layer is to connect the datastore (repository layer) with the delivery layer.
Thus, this layer is also responsible for the validity of data, if something happens invalid data on the repository or delivery,
then this layer will be in the blame.
This layer is really pure must logic (bussiness logic), for example: sum total input,
or nose-compose response where the combination of some repository / model.
This layer depends on the Repository layer. So changes in the repository on a large scale, can affect this layer.

### Delivery Layer
This layer will serve as the presenter or become the output of the application.
This layer is responsible for determining the delivery method that is in use, can with REST API, HTML, gRPC or File etc.
Another task of this layer, because it becomes a connecting wall between the user and the system,
of course, accept all input and validation of inputs according to the standards used.
For the example project I use, I selected REST API as its delivery layer.
So, communication between clien / user to my system is done through REST API


## Installing

    go get github.com/shinichi81/go-monitoring

## move to project

    cd go-monitoring






> Make Sure you have install and run all service

