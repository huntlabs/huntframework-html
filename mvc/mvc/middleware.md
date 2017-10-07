HTTP 中间件
=====

HTTP 中间件提供一个方便的机制来过滤进入应用程序的 HTTP 请求;

Before / After 中间件
-----

添加中间件
-----
```
module app.middleware.apiauth;

import hunt;

class ApiAuthMiddleware : IMiddleware
{
	string name()
	{
		return "ApiAuthMiddleware";
	}

	Response onProcess(Request req,Response res)
	{
		auto uid = req.get("uid",null);
		auto token = req.get("token",null);

		bool status = checkToken(uid,token);
		// 返回null就表明中间件无异常,返回Response 框架会中断后续流程,直接返回处理结果
		if(!status)
		{
			res.html("token error");
			return res;
		}
		else
		{
			return null;
		}

	}
}
```

注册中间件
-----
```
@Action
@Middleware("ApiAuthMiddleware")
void info()
{
}
```
