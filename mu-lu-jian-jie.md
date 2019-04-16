```
.
├── README.md
├── appconf.json // 项目配置
├── apps
│   ├── api
│   │   ├── article
│   │   │   ├── gene.go // 代码解析站位文件
│   │   │   ├── t._define.go // 路由声明，中间件申明文件
│   │   │   └── t.router1.go // 路由实现
│   │   ├── gene.go
│   │   ├── t._define.go
│   │   ├── t.router1.go
│   │   └── t.router2.go
│   ├── gene.go
│   ├── t._define.go
│   ├── t.router1.go
│   └── task
│       ├── gene.go
│       ├── t._define.go
│       ├── t.router1.go
│       └── t.router2.go
├── boot.go // 项目引导代码主文件（自动生成）
├── imports // 项目模块引导文件（自动生成）
│   ├── app_.go
│   ├── app_api.go
│   ├── app_api_article.go
│   └── app_task.go
├── main.go
└── vendor
    └── vendor.json
```



