HTTP 路由
=====

在main函数中调用hunt函数添加路由
-----

封装过的HTTP方法
```
GET(string path,HandleFunction handle);//其他的还有POST,DELETE,PATCH,PUT,HEAD,OPTIONS
```

原始的添加路由函数
```
addRoute(string method, string path, HandleFunction handle, string group = DEFAULT_ROUTE_GROUP);
```

实例
```
//首先定义一个 HandleFunction
void hello(Request req)
{
	Response res = req.createResponse();
	res.html("hello world");
	res.done();
}
//在main函数中添加路由
app.addRoute("GET","/hello",&hello);
```


通过配置文件添加路由
-----
在source同级目录下创建config目录,并添加routes配置文件
```
//项目文件如下
website
  config
    routes
    application.conf
  source
    app.d
  dub.json
```

修改routes文件
```
GET        /                index.index
```

添加index控制器文件(source/app/controller/index.d)
```
module app.controller.index;

import hunt;

class IndexController : Controller
{
	mixin MakeController;

	@Action
	void index()
	{
		response.html("hello world");
	}
}
```


静态文件路由
-----
添加如下配置
```
#method   path          file directory
*        /public        staticDir:public/static
```

路由正则匹配
-----
所有匹配到 `/user/\d+ `的GET请求都会被user.indo处理
```
GET        /user/<id:\d+>            user.info
```

路由参数
-----
```
GET        /user/<id:\d+>/info/<uid:\d+>          user.info
```
取得路由参数
```
auto id = req.getMate("id",null);
auto uid = req.getMate("uid",null);
```


路由组
-----
可以通过两种方式定义路由组
- 一种是调用`addRoute`方法时传递group参数
- 另一组是在`config/application.conf `中添加路由组配置,实例如下
```
//根据域名区分路由组,如下所示,所有api.example.com的请求会分发到api路由组
route.groups = admin:domain:admin.example.com, api:domain:api.example.com
//根据路径区分路由组,如下所示,所有/api/开头的路径的请求会分发到api路由组
route.groups = admin:directory:admin, api:directory:api
```
为路由组添加单独的路由配置文件
```
config
  admin.routes
  api.routes
```
修改admin.routes路由配置文件
```
GET        /                index.index
```
为路由组添加控制器

```
source
  app
    controller
      admin
        index.d
      api
        index.d
```

修改source/app/controller/admin/index.d 为admin路由组添加控制器
```
module app.controller.admin.index;

import hunt;

class IndexController : Controller
{
	mixin MakeController;

	@Action
		void index()
		{ 
			response.html("ADMINCP..");
		}
}
```
