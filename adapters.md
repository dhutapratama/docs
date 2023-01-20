# Adapters

- [Introduction](#introduction)
    - [Adapter Vs. Direct Controller](#adapter-vs-direct-controller)
- [HTTP Adapter](#http-adapter)
- [gRPC Adapter](#grpc-adapter)
- [RabbitMQ Adapter](#rabbitmq-adapter)

<a name="introduction"></a>
## Introduction

Lets's "adapters" berisi definisi data request dan respon data untuk berbagai protokol. `adapters/servers/GrpcAccount.go` perhatikan penamaan protokol yang disertakan diawal nama file untuk memudahkan anda.

Adapter difokuskan untuk berkomunikasi dengan client atau dengan servis lain.

```go
package servers

import (
	"context"
	"encoding/json"
	"fmt"
	"lets-go-framework/app/adapters/data"
	"lets-go-framework/app/adapters/protobuf"
	"lets-go-framework/app/controllers"
	"net/http"
)

type ApiAccountServer struct {
	protobuf.ApiAccountServer
}

func (ApiAccountServer) Insert(ctx context.Context, request *protobuf.RequestAccountInsert) (response *protobuf.ResponseAccountInsert, err error) {
	// Convert protobuf type to data type
	requestJson, _ := json.Marshal(request)

	// Data binding
	var cRequest data.RequestAccountInsert
	json.Unmarshal(requestJson, &cRequest)

	// Call controller
	controllerResponse, err := controllers.AccountInsert(&cRequest)
	if err != nil {
		fmt.Println(err.Error())
		return
	}

	// Convert response data type to protobuf type
	response = &protobuf.ResponseAccountInsert{
		Code:   http.StatusCreated,
		Status: "success",
	}

	return
}
```

Adapter untuk client

```go
package clients

import (
	"context"
	"encoding/json"
	"fmt"
	"lets-go-framework/app/adapters/data"
	"lets-go-framework/app/adapters/protobuf"
	"lets-go-framework/app/controllers"
	"net/http"
)

type ApiAccountServer struct {
	protobuf.ApiAccountServer
}

func (ApiAccountServer) Insert(ctx context.Context, request *protobuf.RequestAccountInsert) (response *protobuf.ResponseAccountInsert, err error) {
	// Convert protobuf type to data type
	requestJson, _ := json.Marshal(request)

	// Data binding
	var cRequest data.RequestAccountInsert
	json.Unmarshal(requestJson, &cRequest)

	// Call controller
	controllerResponse, err := controllers.AccountInsert(&cRequest)
	if err != nil {
		fmt.Println(err.Error())
		return
	}

	// Convert response data type to protobuf type
	response = &protobuf.ResponseAccountInsert{
		Code:   http.StatusCreated,
		Status: "success",
	}

	return
}
```

Setiap request yang masuk akan di handle adapter untuk melakukan data binding dan memanggil controller yang memproses logika.

<a name="adapter-vs-direct-controller"></a>
### Adapter Vs. Direct Controller

The decision to use direct controller will come down to personal taste and the tastes of your development team. Adapter can be used to create robust, well-tested Lets applications. Adapter are not mutually exclusive. Some parts of your applications may use adapter while others depend on protocols. As long as you are keeping your package' responsibilities focused, you will notice very few practical differences between using controllers.

In general, most applications can use controller without issue during development.

<a name="http-adapter"></a>
## HTTP Adapter

```go
package servers

import (
	"lets-go-framework/app/adapters/data"
	"lets-go-framework/app/controllers"
	"lets-go-framework/lets"

	"github.com/gin-gonic/gin"
)

func CreateAccount(g *gin.Context) {
	var err error

	// Bind json body into struct format
	var request data.RequestAccountInsert
	if err = g.Bind(&request); err != nil {
		lets.HttpResponse(g, response, err)
		return
	}

    // Call controller
	var response data.ResponseAccountInsert
	response, err = controllers.AccountInsert(&request)
	if err != nil {
		lets.HttpResponse(g, response, err)
		return
	}

    // Reponse
	lets.HttpResponse(g, response, err)
}
```

<a name="grpc-adapter"></a>
## gRPC Adapter

```go
package servers

import (
	"context"
	"encoding/json"
	"fmt"
	"lets-go-framework/app/adapters/data"
	"lets-go-framework/app/adapters/protobuf"
	"lets-go-framework/app/controllers"
	"net/http"
)

type ApiAccountServer struct {
	protobuf.ApiAccountServer
}

func (ApiAccountServer) Insert(ctx context.Context, request *protobuf.RequestAccountInsert) (response *protobuf.ResponseAccountInsert, err error) {
	// Convert protobuf type to data type
	requestJson, _ := json.Marshal(request)

	// Data binding
	var cRequest data.RequestAccountInsert
	json.Unmarshal(requestJson, &cRequest)

	// Call controller
	controllerResponse, err := controllers.AccountInsert(&cRequest)
	if err != nil {
		fmt.Println(err.Error())
		return
	}

	// Convert response data type to protobuf type
	response = &protobuf.ResponseAccountInsert{
		Code:   http.StatusCreated,
		Status: "success",
	}

	return
}
```

<a name="rabbitmq-adapter"></a>
## RabbitMQ Adapter

```go
package servers

import (
    "fmt"

	"lets-go-framework/app/adapters/data"
	"lets-go-framework/app/controllers"
	"lets-go-framework/lets/rabbitmq"
)

func RabbitAccountInsert(r *rabbitmq.Event) {
	var request = r.GetData().(data.RequestAccountInsert)
	var err error

	// Call controller
	var response data.ResponseAccountInsert
	response, err = controllers.AccountInsert(&request)
	if err != nil {
		fmt.Println("ERR: ", err.Error())
	}

    fmt.Println("Success: ", response)
}
```

