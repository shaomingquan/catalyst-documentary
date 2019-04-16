### 声明一个路由

需要声明 Prefix，Method，Handler 三个要素：

* 声明需在同一个模块内，这个模块要在apps目录下。
* 声明所在的文件需要以`t.`开头，否则不会被解析。
* 同一个路由的声明需要有统一的后缀，这里是`Hello`。
* Prefix，Method，Handler为必要要素，确实其一会在代码生成时报panic。

t.\_define.go：

```go
var PrefixOfHello = "/hello"
var MethodOfHello = "GET,POST"
```

t.router.go

```go
func HandlerOfHello(ctx *gin.Context) {
    ctx.JSON(200, gin.H{
        "message": "this is hello of api",
    })
}
```

tips：

* 若声明多动词需要用逗号分隔，如上`GET,POST`。
* 路由声明会自动以模块所在目录和apps/的相对路径为命名空间，如：
  * 在`apps/api/`下面的声明，prefix为`/hello`，那么真实的挂载路径为`/api/hello`。



