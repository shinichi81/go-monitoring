# go-monitoring

Let’s sum this all up by creating a list of all layers and the parts of our software therein:

Domain:
    Customer entity
    Item entity
    Order entity
Use Cases:
    User entity
    Use case: Add Item to Order
    Use case: Get Items in Order
    Use case: Admin adds Item to Order
Interfaces:
    Web Services for Item/Order handling
    Repositories for Use Cases and Domain entities persistence
Infrastructure:
    The Database
    Code that handles DB connections
    The HTTP server
    Go Standard Library