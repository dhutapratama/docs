# HTTP Server

- [Introduction](#introduction)
- [Konfigurasi](#configuration)
    - [Overriding Environment Variable](#overriding-environment-variable)


<a name="introduction"></a>
## Introduction

Lets framework meggunakan [Gin Web Framework](https://gin-gonic.com/docs/) sebagai handler http request.

<a name="configuration"></a>
## Configuration

Let's take a look at an example of a basic http configurations. Note that the config replace the frameworks.HttpConfig variables included with Lets: `configs/app.go`

```go
func AppConfigs() {
    frameworks.HttpConfig = &types.HttpServer{
        Port:       os.Getenv("SERVE_HTTP_PORT"),
        Middleware: services.MiddlewareHttpService,
        Router:     services.RouteHttpService,
    }
}
```

Jika tidak menginginkan http server untuk berjalan maka anda membuat konfigurasi menjadi tidak bernilai :

```go
func AppConfigs() {
    frameworks.HttpConfig = nil
}
```

<a name="overriding-environment-variable"></a>
### Overriding Environment Variable

Anda dapat mengoverride konfigurasi default dengan mengganti value port secara langsung kedalam variable `Port:`, Let's take a look at an example of a setup :

```go
func AppConfigs() {
    frameworks.HttpConfig = &types.HttpServer{
        Port:       "80", // [string] port number
        Middleware: services.MiddlewareHttpService,
        Router:     services.RouteHttpService,
    }
}
```
