### xCrud

使用xCrud可以满足基础的数据管理crud需求，自动生成数据接口，快速打通前端和数据库。

xCrud基于gorm，但目的并不是以另一种形式覆盖gorm的功能，旨在让特定的功能更简单。

### 添加一组接口

我们需要使用catalyst的crud模版创建xCrud项目，`catalyst new myapp2 -port=8080 -tpl=crud`，在crud模版的store目录下，有xCrud的完整例子。

###### 1，建表，声明gorm model

mysql，gorm基础使用，这里不再赘余。

###### 2，给model加一组生命周期

* SingleInstance，ListInstance：提供model单例和列表原始资料，用作反序列化或者作为gorm查询的结果，没有其他功能。
* NewInstance：创建model实例时调用，用于初始化字段。在使用POST时调用。
* ReturnInstance：返回model列表时调用，用于返回时对列表内元素的格式化，过滤，或者混入信息。在使用GET时调用。

如下：

```go
package store

import (
    "time"

    "github.com/gin-gonic/gin"
)

type InstanceLifecycle struct {
    SingleInstance func(ctx *gin.Context) interface{}
    ListInstance   func(ctx *gin.Context) interface{}

    NewInstance    func(ctx *gin.Context) interface{}
    ReturnInstance func(ctx *gin.Context, ret interface{}) interface{}
}

var modelInstanceMapper = map[string]InstanceLifecycle{
    "test": InstanceLifecycle{
        SingleInstance: func(ctx *gin.Context) interface{} {
            return &Test{}
        },
        ListInstance: func(ctx *gin.Context) interface{} {
            return &[]Test{}
        },
        NewInstance: func(ctx *gin.Context) interface{} {
            // post hook
            // maybe mysql CURRENT_TIME, just for demo
            return &Test{
                CreatedAt: time.Now(),
                UpdatedAt: time.Now(),
            }
        },
        ReturnInstance: func(
            ctx *gin.Context,
            ret interface{},
        ) interface{} {
            // get hook
            // formatter, parser, mixin other data...
            _list := *ret.(*[]Test)
            list := make([]Test, len(_list))

            for index, item := range _list {
                item.Name = item.Name + " ~~"
                list[index] = item
            }
            return list
        },
    },
}
```

###### 3，挂载中间件到路径

在此种情景下，中间件更像是拦截器。

如下：

```go
package apps

var MiddlewaresComposer = []string{

    // crud interseptor
    "store@Crud#/api/data/test/,test",

    "middwares@Demo#root", // pkg@method#param1,param2
}

var PrefixOfRoot = "/"
var MethodOfRoot = "GET"
```

拦截器声明`store@Crud#/api/data/test/,test`：

* 参数1，挂载的路径，保证不冲突。
* 参数2，指定model对应的一组声明周期。



