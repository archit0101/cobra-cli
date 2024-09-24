# julo-go-skeleton
Skeleton code for Go projects that follows Clean Architecture

## Project Structure
### `cmd/app/main.go`
This is where the `main` app resides, as you can see inside the Makefile build script: `go build -o julo-go-skeleton ./cmd/app/`


### `internal/app`
The `Run` function is being called by _main_ from `cmd/app/main.go`. 

Inside the `Run` function, persistent, redis, httpclient and usecase (we call it service) objects are being created here. We implement Dependency Injection using the `New` constructors.

HTTP server is being started in `Run` function as well.

### `internal/controller`
Controller layer, where the request to server is being processed.

### `internal/services`
This is where the business logic happens. Business logic with the same purposes / area should be grouped into a `_service.go` files. 

#### `internal/services/mock`
Mocks for each `service` this ensures the code inside `services` is testable.

We use [mockgen](https://github.com/golang/mock) to generate mocks

Sample command to generate mock:

```sh
$ mockgen -source=internal/services/crud_service.go -package=mock -destination=internal/services/mock/crud_service_mock.go
```

### `internal/repo`
Abstraction and implementation of database action that will be used by the business logic aka `service`

# Updates
- We are introducing an alternative way for generating go projects, [julogen](https://github.com/julofinance/julogen/tree/main), that will use command line interface to automate this process.
- Any future changes planned for julo-go-skeleton must also be made in the julogen [skeletal code](https://github.com/julofinance/julogen/tree/main/cmd/initialize/skeletal), copy of julo-go-skeleton embedded inside julogen.
- Installation
* go install github.com/julofinance/julogen@latest
* julogen create <project_name>
