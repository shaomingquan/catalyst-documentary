### 接口说明

xCrud接口参考restful的动词规范：

POST：

请求体格式为`application/json`并且可以被对应的gorm model反序列化，不会被反序列化的参数会被丢弃。

DELETE：

请求体格式为`application/json`必须含有id，且必须是int类型。

PUT：

在queryString中的query字段指定想要更改的值，格式为`jsonString`，必须含有id，且必须是int类型。

请求体格式为`application/json`包含想要修改字段以及它的最新值，并且可以被正确的反序列化。

GET：

在queryString中的options字段指定想要更改的值，格式为`jsonString`。

```js
{
  "filter": [ // 可以多个组合。
    ["title","abcde","eq"] // 字段，值，操作符。值可以是数字或字符串，字段操作符为字符串。
  ], 
  "sort": [ // 可以多个组合。
    ["create_at","desc"] // 字段，排序方法，默认id降序。
  ],
  "in": {
    "status": [1,4] // 字段，字段值列表。
  },
  "page": 1, // 第几页数据，从1开始。
  "page_count": 10 // 每页的个数。
}
```

##### filter操作符说明：

like：模糊查询。%NBA后缀匹配，NBA%前缀匹配，contains可不加%。

eq：严格等。

lt：小于。

gt：大于。

lte：小于等于。

gte：大于等于。

not：不等于。

_具体请见下面demo：_

### 增删改查demo

增：

```
curl --request POST \
  --url http://localhost:7777/api/data/test/ \
  --header 'Cache-Control: no-cache' \
  --header 'Content-Type: application/json' \
  --header 'Postman-Token: 1a3f8e52-74e4-4a2c-a202-801210a24be2' \
  --data '{"name":"aa","score":80}'
```

删：

```
curl --request DELETE \
  --url http://localhost:7777/api/data/test/ \
  --header 'Cache-Control: no-cache' \
  --header 'Content-Type: application/json' \
  --header 'Postman-Token: cb2d800e-be85-4a87-b512-996d7c05d547' \
  --data '{"id":1}'
```

改：

```
curl --request PUT \
  --url 'http://localhost:7777/api/data/test/?query={%22id%22:1}' \
  --header 'Cache-Control: no-cache' \
  --header 'Content-Type: application/javascript' \
  --header 'Postman-Token: b50a372b-3f60-4748-aaff-8dd57985ad15' \
  --data '{\n    "name": "bb"\n}'
```

查：

```
curl --request GET \
  --url 'http://localhost:7777/api/data/test/?options={%22filter%22:[[%22score%22,%2279%22,%22lte%22]],%22sort%22:[[%22score%22,%22asc%22]]}' \
  --header 'Cache-Control: no-cache' \
  --header 'Postman-Token: 88345134-ccc6-4e5b-b0e2-b520a64d4b7c'
```



