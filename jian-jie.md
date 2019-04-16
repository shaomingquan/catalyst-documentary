### 路由分组、分层级

* 通过组织目录结构的方式将路由分成多个模块以及层级。
* 模块之前存在层级关系，低层级会继承高层级的命名空间和中间件。
* 支持多动词同时定义。

### 命令式中间件、可继承

* 使用高阶函数做“中间件工厂”。
* decorator：最细粒度的中间件。
* 一条“命令”安装卸载中间件。
* 自动继承上层模块中间件，同层不同模块中间件隔离。

### 优雅的参数验证 xParam

* 只需声明参数结构体，xParam会自动将gin的请求参数转换成结构体的实例，使用
  `gin.Get("xParam")`
  获得。
* 使用go官方的validator.v2做参数验证。验证器快速复用。

### 快速添加增删改查接口 xCrud

* 只需要声明符合gorm标准的结构体，定义生命周期函数，即可自动生成crud接口。
* 不覆盖所有场景，针对单表，希望足够好用。

> 请参考项目示例：[https://github.com/shaomingquan/webcore-sample](https://legacy.gitbook.com/book/shaomingquan/catalyst/edit#)



