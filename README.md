# go-monitoring

Let’s sum this all up by creating a list of all layers and the parts of our software therein:

├──delivery                        // Serve content via HTTP? CLI? everything related to that should be here
|   └── http
|       ├── app.go                 // where we have our GIN app
|       ├── app_test.go            // our app tests
|       ├── context                // some gin dependencies
|       |   ├── context.go
|       │   └── mocks
|       │       └── Context.go
|       ├── controllers            // our controllers
│       └── usecase                // our interfaces to the use case layer
│           ├── mocks
│           │   └── Account.go
│           └── account.go
├── domain
│   └── account
│      └── account.go
|
├── infrastructure                 // Where we have our implementation details (Database connections, Queues, External services)
│   └── repository
│       └── awsdynamodb
|           ├── schema
|           |   └── account.go     // Our intermediary data type
|           ├── transformer
|           |   └── account.go     // Where we make our intermediate data types to domain types
|           ├── account.go         // Our dynamodb repository implementation
|           └── account_test.go    // Our dynamodb repository test
|
├── usecase                        // The glue
│   ├── account.go
│   ├── account_test.go
│   └── repository
│       ├── mocks
│       │   └── Account.go
│       └── account.go             // our interface, in the correct layer. Implementations are on
                                   // ./infratructure directory