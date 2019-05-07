> 与gin 的 binding功能类似。使用代码生成去掉了runtime反射，类型没有binding齐全，没有实现yaml，xml类型解析。

### xParams

根据对路由声明的参数结构体，自动的把`queryString，urlencoded，application/json`类型的参数转换类型并且合并为结构体，并使用[https://gopkg.in/validator.v2验证结构体的字段合法性。](https://gopkg.in/validator.v2验证结构体的字段合法性。)

```go
type ParamsOfGetDetail struct {
    ArticleId string  `validate:"nonzero"`
    Version   float64 `validate:"nonzero"`
}

func HandlerOfGetDetail(ctx *gin.Context) {
    _params, _ := ctx.Get("xParams")
    params := _params.(*ParamsOfGetDetail)
    ctx.JSON(200, gin.H{
        "message": "text book",
        "xParams": params,
    })
}
```

在业务逻辑中，使用`xParams`取出参数。一个合法的请求如下，catalyst会把camelcase转成snakecase，再做验证：

`http://localhost:7777/api/article/detail?version=1.2&article_id=abcde`

### 优先级

catalyst会把`queryString，urlencoded，application/json`类型的参数做合并，优先级为：

* queryString
* urlencoded
* application/json

这意味着如果在queryString和uriencoded中同时声明参数a，那么urlencoded重的参数会失效。

二进制类型接口请关闭验证，即不声明`ParamsOfXXX`。

