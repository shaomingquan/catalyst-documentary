### 声明一组中间件

中间件的引入免去了中间件所在包的import，在对应模块的`MiddlewaresComposer`声明中间件引用命令即可：

t\_define.go:

```go
var MiddlewaresComposer = []string{
    "middwares@Demo#root", // pkg@method#param1,param2
}
```

`MiddlewaresComposer`声明一组定制的命令，命令以`包名@方法#参数1,参数2`为格式。middwares是相对于项目根路径的包，如项目的跟路径是`github.com/shaomingquan/catalyst-sample`，那么middwares指`github.com/shaomingquan/catalyst-sample/middwares`。

middwares包中的Demo方法如下：

```go
func Demo(word string) gin.HandlerFunc {
    // initial with string param
    return func(ctx *gin.Context) {
        fmt.Println("START----" + word + "----")
        ctx.Next()
        fmt.Println("END----" + word + "----")
    }
}
```

这样更清晰的展示了中间件初始化的过程。

### 中间件的继承

子模块会自动继承父模块的中间件，还是以`middwares@Demo`这个中间件为例，在模块apps/中声明：

```go
var MiddlewaresComposer = []string{
    "middwares@Demo#root", // pkg@method#param1,param2
}
```

在模块apps/api/中声明：

```go
var MiddlewaresComposer = []string{
    "middwares@Demo#root-api", // pkg@method#param1,param2
}
```

此时apps/作为apps/api/的父模块，中间件被子模块继承，此时访问子模块路由，可以看到中间件被继承。

```
START----root----
START----root-api----
END----root-api----
END----root----
```

catalyst中间件继承的实质是用把目录结构翻译成了gin的api Group。

### decorator，细粒度中间件

灵感来自于python的flask，对于指定路由的decorator，选择把它声明到路由最近的位置。如`DecoratorOfWorld`，声明一组`World`的装饰器。

```go
var DecoratorOfWorld = []string{
    "middwares@Demo#root-api-world-decorator", // pkg@method#param1,param2
}

func HandlerOfWorld(ctx *gin.Context) {
    ctx.JSON(200, gin.H{
        "message": "this is world of api",
    })
}
```



