# datastash

Spring Cloud 微服务，用于接收业务数据日志存入 MongoDB，便于以后数据分析

## Api

### HTTP Request

这个接口为异步接口，收到请求正确解析 json 后直接返回 Http Status 200， 不返回是否成功插入 MongoDB 结果

`POST http://datastash/rpc/stash`

### Request Body (application/json)

```json
{
	"database": "foo",
	"collection": "person",
	"document": {
		"key": "value"
	}
}
```

Property | Require | Description
--------- | ------- | -----------
database | true | The mongodb database name.
collection | true | The mongodb collection name.
document | true | MongoDB document object, can't be array.

## Dep

已将 `vendor` 目录加入版本控制，检出项目后不用安装依赖

如想增加依赖必须使用代理

```bash
$ HTTP_PROXY=<your proxy> dep ensure -add <repository url>
```

## Configuration

项目配置使用系统环境变量，可配置参数如下：

```
Port               int    `env:"DATASTASH_PORT" envDefault:"9999"`
EurekaHost         string `env:"DATASTASH_EUREKA_HOST" envDefault:"http://localhost:8761/eureka"`
MongoURL           string `env:"DATASTASH_MONGO_URL" envDefault:"mongodb://localhost:27017"`
MongoAuthMechanism string `env:"DATASTASH_MONGO_AUTH_MECHANISM" envDefault:"SCRAM-SHA-1"`
MongoUsername      string `env:"DATASTASH_MONGO_USERNAME" envDefault:"admin"`
MongoPassword      string `env:"DATASTASH_MONGO_PASSWORD" envDefault:"admin"`
MongoAuthSource    string `env:"DATASTASH_MONGO_AUTH_SOURCE" envDefault:"admin"`
```