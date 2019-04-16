### 核心技术点

##### 引导代码生成

* go generate：使用go官方的工具链go generate获取包信息，包内文件列表，以便解析。
* ast analysis：对包内的每个文件做语法分析，提取关键。

##### api分组

* gin api grouping：在代码生成阶段，对路由统一收集后按一定的顺序挂载分组。

xParam

* go validator.v2\(v\*\)：在代码生成阶段自动将结构体转化成运行时valid中间件。

### 核心流程

### ![](/assets/flow.png)



