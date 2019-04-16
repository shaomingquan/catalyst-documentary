### 安装运行

1，安装项目所需的命令行工具

`go get -u github.com/shaomingquan/catalyst` 安装catalyst命令行工具。

`go get -u github.com/kardianos/govendor` 安装govendor，用于安装项目依赖。

2，下载模版项目

`catalyst new myapp`。

* `-port`定义项目启动端口，`-tpl`定义初始项目模版。皆可缺省，端口默认7777，模版默认simple，`-tpl=crud`为crud模版。
* 使用catalyst的new命令，紧跟着项目的名字，会在当前目录创建项目目录，并加入初始项目代码。
* 框架会自动验证你的操作目录是否在`$GOPATH/src`下。

3，下载依赖

`cd myapp && govendor sync`请耐心等待。

4，启动

`catalyst dev`

```
[ catalyst ] : clear genfiles ...start
[ catalyst ] : clear genfiles ...done

[ catalyst ] : generate boot.go and importfiles ...start
[ catalyst ] : generate boot.go and importfiles ...done

[ catalyst ] : start dev app ...start
...
...
...
```

访问试试？：

* [http://localhost:7777/api/article/Detail?article\_id=3&version=3](http://localhost:7777/api/article/Detail?article_id=3&version=3)
* [http://localhost:7777/api/Hello](http://localhost:7777/api/Hello)

### 命令行工具介绍

输入`catalyst help`查看帮助文档。

```
hi!


[new]    =>    create new project
    example: catalyst new your-project-name -port=8080 -tpl=crud
        -port: app start port
        -tpl: app start template
            -tpl=curl: curl base tpl


[dev]    =>    run dev server
    example: catalyst dev
        -withoutrun: only gene bootfile


[update] =>    update catalyst runtime lib and clitool
    example: catalyst update
```



