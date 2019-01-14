# httplib

`httplib` is an libary help you to curl remote url.

This lib forked from [beego-httplib](https://github.com/astaxie/beego/tree/develop/httplib), for using without any dependencies.

## Installation

```bash
go get -u github.com/barryz/httplib
```

## How to use

### GET

you can use Get to crawl data.

```go
import "github.com/barryz/httplib"
import "fmt"


func main() {
    req, err := httplib.Get("http://beego.me/")
    if err != nil {
        // error
    }
    str, err := req.String()
    if err != nil {
        // error
    }
    fmt.Println(str)
}
```

### POST

POST data to remote url

```go
import "github.com/barryz/httplib"
import "fmt"


func main() {
    req, err := httplib.Post("http://beego.me/")
    if err != nil {
        // error
    }
    req.Param("username","astaxie")
    req.Param("password","123456")
    str, err := req.String()
    if err != nil {
        // error
    }
    fmt.Println(str)
}
```

### Set timeout

The default timeout is `60` seconds, function prototype:

```go
SetTimeout(connectTimeout, readWriteTimeout time.Duration)
```

Example:

```go
// GET
req, err := httplib.Get("http://beego.me/")
if err != nil {
    // handle error
}
req.SetTimeout(100 * time.Second, 30 * time.Second)

// POST
req, err := httplib.Post("http://beego.me/")
if err != nil {
    // handle error
}
req.SetTimeout(100 * time.Second, 30 * time.Second)
```

### Debug

If you want to debug the request info, set the debug on

```go
req, err := Get("http://beego.me/")
if err != nil {
    // handle error
}
req.Debug(true)
```

### Set HTTP Basic Auth

```go
req, err := Get("http://beego.me/")
if err != nil {
    // handle error
}
str, err := req.SetBasicAuth("user", "passwd").String()
if err != nil {
    // handle error
}
fmt.Println(str)
```

### Set HTTPS

If request url is https, You can set the client support TSL:

```go
httplib.SetTLSClientConfig(&tls.Config{InsecureSkipVerify: true})
```

More info about the `tls.Config` please visit [http://golang.org/pkg/crypto/tls/#Config](http://golang.org/pkg/crypto/tls/#Config).

### Set HTTP Version

some servers need to specify the protocol version of HTTP

```go
httplib.Get("http://beego.me/").SetProtocolVersion("HTTP/1.1")
```

### Set Cookie

some http request need setcookie. So set it like this:

```go
cookie := &http.Cookie{}
cookie.Name = "username"
cookie.Value  = "astaxie"
httplib.Get("http://beego.me/").SetCookie(cookie)
```

### Upload file

httplib support mutil file upload, use `req.PostFile()`

```go
req := httplib.Post("http://beego.me/")
req.Param("username","astaxie")
req.PostFile("uploadfile1", "httplib.pdf")
str, err := req.String()
if err != nil {
    // handle error
}
fmt.Println(str)
```

See godoc for further documentation and examples.

* [godoc.org/github.com/barryz/httplib](https://godoc.org/github.com/barryz/httplib)
