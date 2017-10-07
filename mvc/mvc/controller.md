HTTP 控制器
=====

控制器可以将相应的 HTTP 请求逻辑集合到一个类里面。控制器类一般存放在` source/app/controller `目录下.

基础控制器
-----
这是一个基础控制器的例子:
```
module app.controller.index;
class IndexController : Controller
{
    @Action
	void index()
	{
		response.html("list");
	}
}
```

控制器和模块命名
-----
- 这一点尤其重要
- 在默认路由组的情况下, 当我们添加一条路由指向 ` index.index ` 路由配置时,框架会去寻找`source/app/controller/index.d`文件里的`IndexController`类的`index`方法
- 在设置了路由组的情况下,例如admin路由组, 框架会去寻找`source/app/controller/admin/index.d`文件,同样的module名也相应的为`app.controller.admin.index`
